# hybrid_router.py
import time
from typing import List, Dict, Any

class AdapterError(Exception):
    pass

class BaseAdapter:
    def search(self, origin: str, dest: str, date: str) -> List[Dict[str, Any]]:
        raise NotImplementedError
    def book(self, offer: Dict[str, Any], passenger_info: Dict[str, Any]) -> Dict[str, Any]:
        raise NotImplementedError
    def issue_ticket(self, booking: Dict[str, Any]) -> Dict[str, Any]:
        raise NotImplementedError

class HybridRouter:
    def __init__(self):
        self.adapters = {}  # name -> adapter instance
    def register(self, name: str, adapter: BaseAdapter):
        self.adapters[name] = adapter
    def search_all(self, origin: str, dest: str, date: str) -> List[Dict[str, Any]]:
        results = []
        for name, adapter in self.adapters.items():
            try:
                found = adapter.search(origin, dest, date)
                for r in found:
                    r['_source'] = name
                results.extend(found)
            except Exception as e:
                # important: don't crash whole flow if one provider fails
                results.append({'_source': name, 'error': str(e)})
        # sort / dedupe logic here if needed
        return results

    def book(self, source_name: str, offer: Dict[str, Any], passenger_info: Dict[str, Any]) -> Dict[str, Any]:
        adapter = self.adapters.get(source_name)
        if not adapter:
            raise AdapterError(f"No adapter for {source_name}")
        return adapter.book(offer, passenger_info)

    def issue(self, source_name: str, booking: Dict[str, Any]) -> Dict[str, Any]:
        adapter = self.adapters.get(source_name)
        if not adapter:
            raise AdapterError(f"No adapter for {source_name}")
        return adapter.issue_ticket(booking)
# idempotent_booking.py
import hashlib
import json
import random
import time

def idempotency_key(*parts) -> str:
    raw = "|".join([json.dumps(p, sort_keys=True, ensure_ascii=False) for p in parts])
    return hashlib.sha256(raw.encode('utf-8')).hexdigest()

def retry_with_backoff(fn, max_attempts=5, base_delay=0.5):
    for attempt in range(1, max_attempts + 1):
        try:
            return fn()
        except Exception as e:
            if attempt == max_attempts:
                raise
            sleep_time = base_delay * (2 ** (attempt - 1)) + random.random() * 0.1
            time.sleep(sleep_time)

# Usage example
def place_booking(router: HybridRouter, provider: str, offer: dict, pax: dict, store_lock):
    key = idempotency_key(provider, offer.get('id'), pax.get('email'))
    # store_lock is an abstracted persistence (DB row) marking requests by key
    if store_lock.exists(key):
        return store_lock.get_result(key)

    # obtain logical lock (DB row) to prevent parallel processing
    store_lock.create_pending(key)

    try:
        def _do():
            booking = router.book(provider, offer, pax)
            ticket = router.issue(provider, booking)
            return {'booking': booking, 'ticket': ticket}
        result = retry_with_backoff(_do)
        store_lock.store_result(key, result)
        return result
    except Exception as e:
        store_lock.mark_failed(key, str(e))
        raáie

# reconciliation.py
import pandas as pd

def reconcile_internal_vs_bsp(internal_csv, bsp_csv):
    df_int = pd.read_csv(internal_csv, parse_dates=['issue_date'])
    df_bsp = pd.read_csv(bsp_csv, parse_dates=['issue_date'])

    # normalize key fields
    df_int['key'] = df_int['pnr'].astype(str) + '|' + df_int['ticket_no'].astype(str)
    df_bsp['key'] = df_bsp['pnr'].astype(str) + '|' + df_bsp['ticket_no'].astype(str)

    merged = df_int.merge(df_bsp, on='key', how='outer', suffixes=('_int', '_bsp'), indicator=True)

    mismatches = merged[
        (merged['_merge'] != 'both') |
        (merged['amount_int'].fillna(0) != merged['amount_bsp'].fillna(0)) |
        (merged['status_int'].fillna('') != merged['status_bsp'].fillna(''))
    ]
    # return mismatch report
    return mismatches[['key','pnr_int','ticket_no_int','amount_int','amount_bsp','status_int','status_bsp','_merge']]
# auth_and_audit.py
import secrets
import datetime

class TokenManager:
    # simple in-memory example; in prod use redis or db
    _tokens = {}
    @staticmethod
    def generate(user_id, ttl_seconds=300):
        token = secrets.token_urlsafe(32)
        expire_at = datetime.datetime.utcnow() + datetime.timedelta(seconds=ttl_seconds)
        TokenManager._tokens[token] = {'user_id': user_id, 'expire_at': expire_at}
        return token
    @staticmethod
    def validate(token):
        meta = TokenManager._tokens.get(token)
        if not meta: return False
        if meta['expire_at'] < datetime.datetime.utcnow():
            del TokenManager._tokens[token]
            return False
        return meta['user_id']

class Audit:
    # minimal example: append-only audit. In prod write to append-only DB/table.
    @staticmethod
    def log(action: str, who: str, meta: dict):
        ts = datetime.datetime.utcnow().isoformat()
        entry = {'ts': ts, 'who': who, 'action': action, 'meta': meta}
        # append to file (or dedicated audit table)
        with open('audit.log', 'a', encoding='utf-8') as f:
            f.write(json.dumps(entry, ensure_ascii=False) + '\n')
-- unified view for reporting
CREATE TABLE airlines_gds (
  id INT PRIMARY KEY AUTO_INCREMENT,
  code VARCHAR(10),
  name VARCHAR(255),
  active BOOLEAN DEFAULT TRUE
);
CREATE TABLE airlines_ndc (
  id INT PRIMARY KEY AUTO_INCREMENT,
  code VARCHAR(10),
  name VARCHAR(255),
  active BOOLEAN DEFAULT TRUE
);
CREATE TABLE airlines_lcc (
  id INT PRIMARY KEY AUTO_INCREMENT,
  code VARCHAR(10),
  name VARCHAR(255),
  active BOOLEAN DEFAULT TRUE
);

CREATE VIEW airlines_hybrid_api AS
SELECT 'GDS' as src, id, code, name, active FROM airlines_gds
UNION ALL
SELECT 'NDC' as src, id, code, name, active FROM airlines_ndc
UNION ALL
SELECT 'LCC' as src, id, code, name, active FROM airlines_lcc;


