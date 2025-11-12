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


