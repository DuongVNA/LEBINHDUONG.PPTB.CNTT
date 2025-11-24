<!doctype html>
<html lang="vi">
 <head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>AeroCore Flight Booking System</title>
  <script src="/_sdk/data_sdk.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.min.js"></script>
  <style>
body {
  box-sizing: border-box;
  margin: 0;
  background: #041321;
  min-height: 100%;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  color: #FFFFFF;
}

html, body {
  height: 100%;
}

/* NAVBAR */
.navbar {
  background: #0B2840;
  color: white;
  padding: 20px 32px;
  display: flex;
  align-items: center;
  gap: 8px;
  font-weight: 600;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
  position: sticky;
  top: 0;
  z-index: 1000;
  border-bottom: 2px solid #FFD451;
  overflow-x: auto;
  overflow-y: hidden;
  scroll-behavior: smooth;
  -webkit-overflow-scrolling: touch;
  scrollbar-width: none;
  -ms-overflow-style: none;
}

.navbar::-webkit-scrollbar {
  display: none;
}

.navbar-brand {
  font-size: 24px;
  font-weight: 800;
  margin-right: 32px;
  display: flex;
  align-items: center;
  gap: 8px;
  color: #FFD451;
}

.nav-link {
  color: #E5E7EB;
  text-decoration: none;
  padding: 10px 20px;
  border-radius: 8px;
  transition: all 0.3s ease;
  cursor: pointer;
  font-size: 15px;
  position: relative;
  white-space: nowrap;
}

.nav-link:hover {
  background: rgba(255, 212, 81, 0.1);
  color: #FFD451;
  transform: translateY(-2px);
}

.nav-link.active {
  background: #FFD451;
  color: #041321;
  font-weight: 700;
}

/* PAGE CONTAINER */
.page {
  padding: 40px 24px;
  max-width: 1200px;
  margin: 0 auto;
  min-height: calc(100% - 80px);
  position: relative;
  width: 100%;
  transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1), opacity 0.4s ease;
  opacity: 1;
  transform: translateX(0);
}

.page.hidden {
  display: none;
}

.page.slide-out-left {
  transform: translateX(-100%);
  opacity: 0;
}

.page.slide-out-right {
  transform: translateX(100%);
  opacity: 0;
}

.page.slide-in-left {
  transform: translateX(-100%);
  opacity: 0;
}

.page.slide-in-right {
  transform: translateX(100%);
  opacity: 0;
}

.page.active {
  transform: translateX(0);
  opacity: 1;
}

.pages-wrapper {
  position: relative;
  overflow: hidden;
  min-height: calc(100% - 80px);
}

.page-title {
  font-size: 32px;
  font-weight: 800;
  color: #FFD451;
  margin-bottom: 24px;
  text-shadow: 0 2px 10px rgba(255, 212, 81, 0.3);
}

/* SEARCH BOX */
.search-box {
  background: #0B2840;
  padding: 32px;
  border-radius: 20px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.5);
  max-width: 600px;
  margin: 0 auto;
  border: 2px solid #FFD451;
}

.form-group {
  margin-bottom: 16px;
}

.form-label {
  display: block;
  font-weight: 600;
  margin-bottom: 6px;
  color: #E5E7EB;
}

.form-input {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #4CC9F0;
  border-radius: 10px;
  font-size: 15px;
  box-sizing: border-box;
  transition: all 0.3s ease;
  background: #041321;
  color: #FFFFFF;
}

.form-input:focus {
  outline: none;
  border-color: #FFD451;
  box-shadow: 0 0 0 4px rgba(255, 212, 81, 0.2);
  background: #0B2840;
}

.btn {
  padding: 14px 28px;
  border-radius: 12px;
  font-weight: 700;
  cursor: pointer;
  border: none;
  font-size: 16px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
}

.btn-primary {
  background: #FFD451;
  color: #041321;
  width: 100%;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(255, 212, 81, 0.4);
  background: #EAB308;
}

.btn-primary:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
}

.btn-secondary {
  background: #3A86FF;
  color: white;
}

.btn-secondary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(58, 134, 255, 0.4);
  background: #4CC9F0;
}

.btn-danger {
  background: #ef4444;
  color: white;
}

.btn-danger:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(239, 68, 68, 0.4);
  background: #dc2626;
}

.btn-success {
  background: #10b981;
  color: white;
}

.btn-success:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(16, 185, 129, 0.4);
  background: #059669;
}

/* RESULT CARD */
.result-card {
  background: #0B2840;
  padding: 24px;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  margin-bottom: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
  border: 2px solid #4CC9F0;
}

.result-card:hover {
  border-color: #FFD451;
  transform: translateY(-4px);
  box-shadow: 0 20px 50px rgba(255, 212, 81, 0.3);
}

.flight-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
}

.airline-name {
  font-size: 20px;
  font-weight: 800;
  color: #FFD451;
}

.flight-price {
  font-size: 24px;
  font-weight: 800;
  color: #4CC9F0;
}

.flight-route {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  gap: 16px;
  align-items: center;
  margin-bottom: 12px;
}

.flight-time {
  text-align: center;
}

.time {
  font-size: 20px;
  font-weight: 700;
  color: #FFFFFF;
}

.airport {
  font-size: 13px;
  color: #E5E7EB;
  margin-top: 4px;
}

.flight-duration {
  text-align: center;
  padding: 8px 12px;
  background: rgba(76, 201, 240, 0.2);
  border-radius: 8px;
  border: 1px solid #4CC9F0;
}

.duration {
  font-size: 14px;
  font-weight: 600;
  color: #4CC9F0;
}

.flight-details {
  display: flex;
  gap: 16px;
  font-size: 13px;
  color: #E5E7EB;
  padding-top: 12px;
  border-top: 1px solid rgba(76, 201, 240, 0.3);
}

/* PASSENGER FORM */
.passenger-box {
  background: #0B2840;
  padding: 24px;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  margin-bottom: 20px;
  border: 2px solid #FFD451;
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}

/* BOOKING INFO */
.info-box {
  background: #0B2840;
  padding: 28px;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  margin-bottom: 24px;
  border: 2px solid #4CC9F0;
}

.info-row {
  display: flex;
  justify-content: space-between;
  padding: 12px 0;
  border-bottom: 1px solid rgba(76, 201, 240, 0.2);
}

.info-row:last-child {
  border-bottom: none;
}

.info-label {
  color: #E5E7EB;
  font-weight: 500;
}

.info-value {
  color: #FFFFFF;
  font-weight: 700;
}

.pnr-display {
  font-size: 42px;
  font-weight: 900;
  color: #FFD451;
  letter-spacing: 4px;
  text-align: center;
  padding: 24px 0;
  text-shadow: 0 0 20px rgba(255, 212, 81, 0.5);
}

/* TICKET */
.ticket {
  background: #0B2840;
  padding: 28px;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  margin-bottom: 24px;
  border: 3px solid #FFD451;
}

.ticket-number {
  margin-top: 16px;
  padding: 12px;
  background: rgba(76, 201, 240, 0.2);
  border: 2px solid #4CC9F0;
  border-radius: 8px;
  font-weight: 700;
  color: #4CC9F0;
  font-size: 18px;
  text-align: center;
  letter-spacing: 1px;
}

.qr-container {
  margin-top: 20px;
  text-align: center;
}

.qr-code {
  width: 150px;
  height: 150px;
  background: white;
  border: 2px solid #FFD451;
  border-radius: 8px;
  display: inline-block;
  padding: 8px;
}

/* ALERT */
.alert {
  padding: 16px 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  font-size: 15px;
}

.alert-success {
  background: rgba(76, 201, 240, 0.2);
  border: 2px solid #4CC9F0;
  color: #4CC9F0;
}

.alert-error {
  background: rgba(239, 68, 68, 0.2);
  border: 2px solid #ef4444;
  color: #fca5a5;
}

.alert-info {
  background: rgba(255, 212, 81, 0.2);
  border: 2px solid #FFD451;
  color: #FFD451;
}

/* MESSAGE */
.message {
  margin-top: 16px;
  font-size: 15px;
  text-align: center;
  font-weight: 600;
}

.message.error {
  color: #fca5a5;
}

.message.success {
  color: #4CC9F0;
}

.message.info {
  color: #FFD451;
}

/* TOAST NOTIFICATIONS */
.toast-container {
  position: fixed;
  top: 20px;
  right: 20px;
  z-index: 10001;
  display: flex;
  flex-direction: column;
  gap: 12px;
  pointer-events: none;
}

.toast {
  background: #0B2840;
  border: 2px solid #4CC9F0;
  border-radius: 12px;
  padding: 16px 20px;
  min-width: 300px;
  max-width: 400px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  gap: 12px;
  pointer-events: auto;
  animation: slideInRight 0.3s ease;
  transition: all 0.3s ease;
}

.toast.toast-success {
  border-color: #10b981;
}

.toast.toast-error {
  border-color: #ef4444;
}

.toast.toast-info {
  border-color: #FFD451;
}

.toast.toast-warning {
  border-color: #f59e0b;
}

.toast-icon {
  font-size: 24px;
  flex-shrink: 0;
}

.toast-content {
  flex: 1;
}

.toast-title {
  font-weight: 700;
  font-size: 15px;
  margin-bottom: 4px;
}

.toast-message {
  font-size: 13px;
  color: #E5E7EB;
}

.toast-close {
  background: none;
  border: none;
  color: #E5E7EB;
  font-size: 20px;
  cursor: pointer;
  padding: 0;
  width: 24px;
  height: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  transition: all 0.2s ease;
}

.toast-close:hover {
  background: rgba(255, 255, 255, 0.1);
  color: #FFFFFF;
}

@keyframes slideInRight {
  from {
    transform: translateX(400px);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

@keyframes slideOutRight {
  from {
    transform: translateX(0);
    opacity: 1;
  }
  to {
    transform: translateX(400px);
    opacity: 0;
  }
}

/* DASHBOARD */
.dashboard-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 24px;
  margin-bottom: 32px;
}

.metric-card {
  background: #0B2840;
  padding: 28px;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  border: 2px solid #FFD451;
  transition: all 0.3s ease;
}

.metric-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 50px rgba(255, 212, 81, 0.3);
  border-color: #4CC9F0;
}

.metric-label {
  font-size: 14px;
  color: #E5E7EB;
  margin-bottom: 12px;
  font-weight: 600;
}

.metric-value {
  font-size: 36px;
  font-weight: 900;
  color: #FFD451;
}

.metric-change {
  font-size: 13px;
  margin-top: 8px;
}

.metric-change.up {
  color: #4CC9F0;
}

.metric-change.down {
  color: #ef4444;
}

/* MERMAID DIAGRAM */
.mermaid-container {
  background: #041321;
  padding: 24px;
  border-radius: 12px;
  border: 2px solid #4CC9F0;
  overflow-x: auto;
  margin-bottom: 24px;
}

/* LOADING SPINNER */
.spinner {
  border: 3px solid rgba(76, 201, 240, 0.3);
  border-top: 3px solid #4CC9F0;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  animation: spin 1s linear infinite;
  margin: 20px auto;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

/* STATUS BADGE */
.status-badge {
  display: inline-block;
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 700;
  text-transform: uppercase;
}

.status-confirmed {
  background: rgba(16, 185, 129, 0.2);
  color: #10b981;
  border: 1px solid #10b981;
}

.status-cancelled {
  background: rgba(239, 68, 68, 0.2);
  color: #ef4444;
  border: 1px solid #ef4444;
}

.status-checked-in {
  background: rgba(76, 201, 240, 0.2);
  color: #4CC9F0;
  border: 1px solid #4CC9F0;
}

/* MODAL */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10000;
  padding: 20px;
}

.modal-content {
  background: #0B2840;
  padding: 32px;
  border-radius: 16px;
  max-width: 500px;
  width: 100%;
  border: 2px solid #FFD451;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.8);
}

.modal-title {
  font-size: 24px;
  font-weight: 800;
  color: #FFD451;
  margin-bottom: 20px;
}

.modal-buttons {
  display: flex;
  gap: 12px;
  margin-top: 24px;
}

/* USER INFO */
.user-info {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-left: auto;
  padding: 8px 16px;
  background: rgba(76, 201, 240, 0.1);
  border-radius: 8px;
  border: 1px solid #4CC9F0;
}

.user-email {
  color: #4CC9F0;
  font-weight: 600;
  font-size: 14px;
}

.logout-btn {
  background: #ef4444;
  color: white;
  padding: 6px 12px;
  border-radius: 6px;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  border: none;
  transition: all 0.3s ease;
}

.logout-btn:hover {
  background: #dc2626;
  transform: translateY(-1px);
}

/* RESPONSIVE */
@media (max-width: 768px) {
  .form-grid {
    grid-template-columns: 1fr;
  }
  
  .flight-route {
    grid-template-columns: 1fr;
    gap: 12px;
  }
  
  .navbar {
    flex-wrap: wrap;
    gap: 12px;
  }
  
  .user-info {
    width: 100%;
    justify-content: space-between;
  }
}
</style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="/_sdk/element_sdk.js" type="text/javascript"></script>
  <script src="https://cdn.tailwindcss.com" type="text/javascript"></script>
 </head>
 <body><!-- SECURITY HEADER BAR -->
  <div style="width:100%;background:#0B2840;border-bottom:2px solid #FFD451;padding:8px 16px;display:flex;align-items:center;gap:12px;flex-wrap:wrap;position:fixed;top:0;left:0;z-index:10000"><span style="color:#FFD451;font-weight:800;font-size:18px">LÊ BÌNH DƯƠNG</span>
   <div id="realtimeClock" style="background:#041321;padding:6px 16px;border-radius:8px;border:1px solid #4CC9F0;display:flex;align-items:center;gap:8px;font-size:14px"><span style="color:#4CC9F0;font-weight:700">🕐</span> <span id="clockDisplay" style="color:#FFFFFF;font-weight:600;font-family:monospace;letter-spacing:0.5px">--:--:--</span> <span id="dateDisplay" style="color:#E5E7EB;font-size:13px">--/--/----</span>
   </div>
   <div style="margin-left:auto;background:#041321;padding:6px 16px;border-radius:8px;border:1px solid #FFD451;display:flex;align-items:center;gap:8px;font-size:13px"><span style="color:#10b981;font-weight:700">● LIVE</span> <span style="color:#FFFFFF">• 3DS2 • Anti-bot</span> <span style="color:#E5E7EB">PCI-DSS • 3DS2 • AES-256 • KYC • Anti-fraud</span>
    <svg width="18" height="18" fill="#FFD451" viewbox="0 0 24 24"><rect x="6" y="11" width="12" height="12" rx="2" /> <path d="M8 11V7a4 4 0 0 1 8 0v4" />
    </svg>
   </div>
  </div><!-- NAVBAR -->
  <nav class="navbar" style="margin-top:50px">
   <div class="navbar-brand">
    ✈️ AeroCore
   </div><a class="nav-link active" onclick="navigateTo('search')">Search</a> <a class="nav-link" onclick="navigateTo('passenger')">Passenger</a> <a class="nav-link" onclick="navigateTo('payment')">Payment</a> <a class="nav-link" onclick="navigateTo('mybookings')">My Bookings</a> <a class="nav-link" onclick="navigateTo('dashboard')">Dashboard</a>
   <div class="user-info" id="userInfo" style="display:none"><span class="user-email" id="userEmail"></span> <button class="logout-btn" onclick="logout()">Logout</button>
   </div>
  </nav><!-- PAGES WRAPPER -->
  <div class="pages-wrapper"><!-- LOGIN PAGE -->
   <div id="pageLogin" class="page hidden">
    <h2 class="page-title" style="text-align:center">��� Đăng nhập</h2>
    <div class="search-box">
     <h3 style="margin-top:0;color:#FFD451;font-size:24px;font-weight:800">Thông tin đăng nhập</h3>
     <div class="form-group"><label class="form-label" for="loginEmail">Email</label> <input class="form-input" id="loginEmail" type="email" placeholder="your@email.com">
     </div>
     <div class="form-group"><label class="form-label" for="loginName">Họ tên</label> <input class="form-input" id="loginName" placeholder="Nguyễn Văn A">
     </div><button class="btn btn-primary" onclick="doLogin()">Đăng nhập</button>
     <div id="loginMessage" class="message"></div>
    </div>
   </div><!-- SEARCH PAGE -->
   <div id="pageSearch" class="page active">
    <h2 class="page-title" style="text-align:center">🔍 Tìm kiếm chuyến bay</h2>
    <div class="search-box">
     <h3 style="margin-top:0;color:#FFD451;font-size:24px;font-weight:800">Thông tin chuyến bay</h3>
     <div class="form-group"><label class="form-label" for="searchFrom">From</label> <input class="form-input" id="searchFrom" placeholder="SGN - Tan Son Nhat" value="SGN">
     </div>
     <div class="form-group"><label class="form-label" for="searchTo">To</label> <input class="form-input" id="searchTo" placeholder="HAN - Noi Bai" value="HAN">
     </div>
     <div class="form-group"><label class="form-label" for="searchDate">Date</label> <input class="form-input" id="searchDate" type="date">
     </div><button class="btn btn-primary" onclick="doSearch()">Search Flights</button>
     <div id="searchMessage" class="message"></div>
    </div>
    <div id="searchResults" style="margin-top:24px;max-width:700px;margin-left:auto;margin-right:auto"></div>
   </div><!-- PASSENGER PAGE -->
   <div id="pagePassenger" class="page hidden">
    <h2 class="page-title">��� Thông tin hành khách</h2>
    <div id="passengerForms"></div>
    <div style="margin-top:20px;display:flex;gap:12px"><button class="btn" style="background:#4CC9F0;color:#041321;flex:1;font-weight:700" onclick="addPassenger()">+ Thêm hành khách</button> <button class="btn" style="background:#ef4444;color:white;flex:1;font-weight:700" onclick="removePassenger()">− B��t hành khách</button>
    </div><button class="btn btn-secondary" style="width:100%;margin-top:12px" onclick="navigateTo('search')">← Back to Search</button> <button class="btn btn-primary" style="width:100%;margin-top:12px" onclick="goToPayment()">Tiếp tục → Payment</button>
    <div id="passengerMessage" class="message"></div>
   </div><!-- PAYMENT PAGE -->
   <div id="pagePayment" class="page hidden">
    <div style="max-width:600px;margin:0 auto">
     <h2 class="page-title" style="text-align:center">💳 Thanh toán</h2>
     <div class="info-box">
      <h3 style="margin-top:0;color:#FFD451;font-weight:800">Tổng thanh toán</h3>
      <div style="text-align:center;padding:20px 0">
       <div style="font-size:48px;font-weight:800;color:#4CC9F0" id="paymentTotal">
        ---
       </div>
       <div style="font-size:14px;color:#E5E7EB;margin-top:8px" id="paymentDetails">
        ---
       </div>
      </div>
     </div>
     <div class="search-box">
      <h3 style="margin-top:0;color:#FFD451;font-size:20px;font-weight:800">Email xác nhận</h3>
      <div class="form-group"><label class="form-label" for="confirmEmail">Email nhận vé</label> <input class="form-input" id="confirmEmail" type="email" placeholder="your@email.com">
      </div>
     </div><button class="btn btn-secondary" style="width:100%;margin-bottom:12px" onclick="navigateTo('passenger')">← Quay lại</button> <button class="btn btn-primary" style="width:100%" id="paymentSubmitBtn" onclick="submitPayment()">Xác nhận đặt vé</button>
     <div id="paymentMessage" class="message"></div>
    </div>
   </div><!-- MY BOOKINGS PAGE -->
   <div id="pageMybookings" class="page hidden">
    <h2 class="page-title" style="text-align:center">📋 Booking của tôi</h2>
    <div id="loadingBookings" style="display:none">
     <div class="spinner"></div>
     <p style="text-align:center;color:#E5E7EB">Đang tải booking...</p>
    </div>
    <div id="bookingsList"></div>
    <div id="noBookings" style="display:none;text-align:center;padding:60px 20px">
     <div style="font-size:64px;margin-bottom:20px">
      ✈️
     </div>
     <h3 style="color:#FFD451;font-size:24px;margin-bottom:12px">Chưa có booking nào</h3>
     <p style="color:#E5E7EB;margin-bottom:24px">Hãy tìm kiếm và đặt chuyến bay đầu tiên của bạn!</p><button class="btn btn-primary" style="max-width:300px;margin:0 auto" onclick="navigateTo('search')">Tìm chuyến bay</button>
    </div>
   </div><!-- DASHBOARD PAGE -->
   <div id="pageDashboard" class="page hidden">
    <h2 class="page-title" style="text-align:center">📊 Dashboard</h2>
    <p style="color:#E5E7EB;margin-bottom:30px;text-align:center;font-size:16px">Biểu đồ – số liệu – sequence diagram</p><!-- SEQUENCE DIAGRAM SD1 -->
    <div class="info-box" style="margin-bottom:32px">
     <h3 style="margin-top:0;color:#FFD451;font-weight:800">🔄 SD1 — Search → Availability Flow</h3>
     <div class="mermaid-container">
      <pre class="mermaid">sequenceDiagram
    autonumber
    actor User
    participant Frontend
    participant APIGateway
    participant SearchService
    participant Router
    participant NDC
    participant GDS
    participant PricingService
    participant AvailabilityService
    
    User-&gt;&gt;Frontend: Enter search info
    Frontend-&gt;&gt;APIGateway: GET /search
    APIGateway-&gt;&gt;SearchService: search(params)
    SearchService-&gt;&gt;Router: fan-out providers
    Router-&gt;&gt;NDC: search request
    Router-&gt;&gt;GDS: search request
    NDC--&gt;&gt;Router: search results
    GDS--&gt;&gt;Router: search results
    Router--&gt;&gt;SearchService: normalized results
    SearchService-&gt;&gt;PricingService: calculate final price
    PricingService--&gt;&gt;SearchService: priced offers
    SearchService--&gt;&gt;APIGateway: search response
    APIGateway--&gt;&gt;Frontend: offers list
    Frontend--&gt;&gt;User: show offers
    User-&gt;&gt;Frontend: choose offer
    Frontend-&gt;&gt;APIGateway: POST /availability/check
    APIGateway-&gt;&gt;AvailabilityService: check availability
    AvailabilityService-&gt;&gt;Router: re-verify provider
    Router-&gt;&gt;NDC: availability request
    NDC--&gt;&gt;Router: availability OK
    Router--&gt;&gt;AvailabilityService: availability result
    AvailabilityService--&gt;&gt;APIGateway: availability_token + OK
    APIGateway--&gt;&gt;Frontend: OK
      </pre>
     </div>
    </div><!-- SEQUENCE DIAGRAM SD2 -->
    <div class="info-box" style="margin-bottom:32px">
     <h3 style="margin-top:0;color:#FFD451;font-weight:800">💳 SD2 — Checkout (ShadowPNR → Payment → Booking)</h3>
     <div class="mermaid-container">
      <pre class="mermaid">sequenceDiagram
    autonumber
    actor User
    participant Frontend
    participant APIGateway
    participant ShadowPNRService
    participant PaymentService
    participant FraudEngine
    participant PaymentGateway
    participant BookingService
    participant ProviderAPI
    participant DB
    
    User-&gt;&gt;Frontend: Press "Book"
    Frontend-&gt;&gt;APIGateway: POST /shadow_pnrs
    APIGateway-&gt;&gt;ShadowPNRService: create shadow
    ShadowPNRService-&gt;&gt;DB: save snapshot
    DB--&gt;&gt;ShadowPNRService: saved
    ShadowPNRService--&gt;&gt;APIGateway: shadow_pnr_token
    APIGateway--&gt;&gt;Frontend: token
    Frontend-&gt;&gt;APIGateway: POST /shadow_pnrs/{token}/passengers
    APIGateway-&gt;&gt;ShadowPNRService: attach pax
    ShadowPNRService-&gt;&gt;DB: save passengers
    Frontend-&gt;&gt;APIGateway: POST /payments
    APIGateway-&gt;&gt;FraudEngine: score risk
    FraudEngine--&gt;&gt;APIGateway: low_risk
    APIGateway-&gt;&gt;PaymentService: create payment
    PaymentService-&gt;&gt;PaymentGateway: authorize/3DS
    PaymentGateway--&gt;&gt;PaymentService: success
    PaymentService-&gt;&gt;DB: save payment
    Frontend-&gt;&gt;APIGateway: POST /bookings
    APIGateway-&gt;&gt;BookingService: create booking
    BookingService-&gt;&gt;ProviderAPI: CreatePNR
    ProviderAPI--&gt;&gt;BookingService: PNR=ABC123
    BookingService-&gt;&gt;DB: save booking
    BookingService--&gt;&gt;APIGateway: BOOKED
      </pre>
     </div>
    </div><!-- SEQUENCE DIAGRAM SD3 -->
    <div class="info-box" style="margin-bottom:32px">
     <h3 style="margin-top:0;color:#FFD451;font-weight:800">🎫 SD3 — Ticketing Flow</h3>
     <div class="mermaid-container">
      <pre class="mermaid">sequenceDiagram
    autonumber
    participant BookingService
    participant TicketingService
    participant ProviderAPI
    participant DB
    participant NotificationService
    participant UserEmail
    
    BookingService-&gt;&gt;TicketingService: BookingCreated(PNR)
    TicketingService-&gt;&gt;ProviderAPI: RetrievePNR
    ProviderAPI--&gt;&gt;TicketingService: PNR details
    TicketingService-&gt;&gt;ProviderAPI: issueTicket(PNR)
    ProviderAPI--&gt;&gt;TicketingService: ticket_number
    TicketingService-&gt;&gt;ProviderAPI: issueEMD
    ProviderAPI--&gt;&gt;TicketingService: emd_numbers
    TicketingService-&gt;&gt;DB: save tickets
    DB--&gt;&gt;TicketingService: OK
    TicketingService-&gt;&gt;NotificationService: prepare email
    NotificationService-&gt;&gt;UserEmail: send PDF
      </pre>
     </div>
    </div>
    <div class="dashboard-grid">
     <div class="metric-card">
      <div class="metric-label">
       Tổng tìm kiếm
      </div>
      <div class="metric-value" id="metricSearches">
       8,542
      </div>
      <div class="metric-change up">
       ↑ 423 hôm nay
      </div>
     </div>
     <div class="metric-card">
      <div class="metric-label">
       Tổng đặt vé
      </div>
      <div class="metric-value" id="metricBookings">
       0
      </div>
      <div class="metric-change up">
       ↑ 0 hôm nay
      </div>
     </div>
     <div class="metric-card">
      <div class="metric-label">
       Tỷ lệ chuyển đổi
      </div>
      <div class="metric-value" id="metricConversion">
       0%
      </div>
      <div class="metric-change up">
       ↑ 0%
      </div>
     </div>
     <div class="metric-card">
      <div class="metric-label">
       Doanh thu hôm nay
      </div>
      <div class="metric-value" id="metricRevenue">
       $0
      </div>
      <div class="metric-change up">
       ↑ $0
      </div>
     </div>
    </div>
    <div class="info-box">
     <h3 style="margin-top:0;color:#FFD451;font-weight:800">Hoạt động gần đây</h3>
     <div class="info-row"><span class="info-label">Phiên hoạt động</span> <span class="info-value">1,247</span>
     </div>
     <div class="info-row"><span class="info-label">Đang chờ xử lý</span> <span class="info-value">34</span>
     </div>
     <div class="info-row"><span class="info-label">Hoàn thành hôm nay</span> <span class="info-value">892</span>
     </div>
     <div class="info-row"><span class="info-label">Yêu cầu thất bại</span> <span class="info-value">3</span>
     </div>
    </div><!-- FEATURES TABLE -->
    <div class="info-box" style="margin-top:32px">
     <h3 style="margin-top:0;color:#FFD451;font-weight:800;margin-bottom:20px">⚡ Tính năng hệ thống AeroCore (99 tính năng)</h3>
     <div style="overflow-x:auto;margin-bottom:24px">
      <table style="width:100%;border-collapse:collapse;font-size:13px">
       <thead>
        <tr style="background:#041321;color:#FFD451;font-weight:700">
         <th style="padding:12px 8px;border:1px solid #4CC9F0;text-align:left;width:33%">Tìm kiếm &amp; Đặt vé</th>
         <th style="padding:12px 8px;border:1px solid #4CC9F0;text-align:left;width:33%">Quản lý &amp; Dịch vụ</th>
         <th style="padding:12px 8px;border:1px solid #4CC9F0;text-align:left;width:33%">Nâng cao &amp; Tích hợp</th>
        </tr>
       </thead>
       <tbody style="color:#E5E7EB">
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">✈️ Tìm chuyến bay thường</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💰 Tìm giá thấp nhất</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📅 Tìm giá theo tháng</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🌍 Pricing engine theo nhiều thị trường</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💱 Hỗ trợ multi-currency (VND, USD, EUR…)</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔒 Đặt giữ chỗ</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔄 Đặt lại chỗ</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📖 Mở đặt chỗ</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">❌ Hủy đặt chỗ</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🧳 Đặt hành lý</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💺 Đặt chỗ ngồi</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">➕ Thêm dịch vụ bổ sung</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🧮 Tính giá đặt chỗ</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔀 Đổi chuyến bay</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">✏️ Sửa hành khách</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">👥 Tách hành khách</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">👶 Thêm trẻ sơ sinh</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">➕ Thêm thêm thành viên</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🛂 Cập nhật hộ chiếu</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📞 Cập nhật liên hệ</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📧 Gửi email hãng</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📝 Thêm ghi chú</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">✅ Check-in online</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📦 Gửi đơn hàng</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🎫 Xuất vé</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📄 Xuất EMD</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🖨️ In mặt vé</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🚫 Hủy vé</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔄 Đổi vé</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💸 Hoàn vé</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">⚡ Void vé</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📊 Quản lý đơn hàng</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🗂️ Quản lý đặt chỗ</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🎟️ Quản lý vé xuất</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">👤 Quản lý khách hàng</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔐 Quản lý tài khoản</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🏢 Quản lý chi nhánh</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🏛️ Quản lý phòng ban</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">👔 Quản lý nhân sự</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔑 Phân quyền sử dụng</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">��� Quản lý doanh nghiệp</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📜 Nhật ký audit log</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💲 Chính sách giá</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💵 Phí dịch vụ</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📋 Điều kiện vé</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📬 Cài đặt email</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🎨 Tùy chỉnh mặt vé</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🛡️ Chặn booking trùng lặp</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🎁 Mã khuyến mại</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🌐 Ngôn ngữ đa ngôn ngữ</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💹 Cài đặt tỷ giá</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🏦 Đại lý F1: Nạp tiền, Quản lý quỹ</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💳 Đại lý F2: Nạp tiền xuất vé</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💰 Quản lý ký quỹ</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📊 Quản lý công nợ</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🧾 Xuất hóa đơn</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📑 Quản lý hóa đơn</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔄 Đối soát BSP/ARC</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💳 Thanh toán thẻ Visa/Master/JCB/Amex</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📱 Thanh toán QR (Momo, ZaloPay, VietQR)</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">↩️ Hoàn tiền tự động gateway</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🛡️ Chống gian lận thẻ</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔐 Hỗ trợ 2FA/OTP</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🌐 Cài đặt website</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📝 Quản lý nội dung</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📈 Báo cáo tổng hợp</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📊 Báo cáo đặt chỗ</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📋 Báo cáo xuất vé</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔍 Báo cáo tìm kiếm</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💬 Báo cáo tư vấn</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">⭐ Quản lý khách hàng thân thiết</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🎯 Tích điểm – sử dụng điểm</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🏅 Phân hạng thẻ</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💌 CRM – Email chăm sóc khách hàng</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🍽️ Suất ăn</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🛋️ Phòng chờ sân bay</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">⚡ Fast track</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🚗 Xe đưa đón sân bay</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🛡️ Bảo hiểm</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">📶 eSIM</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔍 Look máy bay</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🛫 Quản lý sân bay (IATA code)</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">ℹ️ Thông tin chuyến bay</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔌 Kết nối NDC</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🎨 Hiển thị rich content</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🔗 Tích hợp thêm API</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">⚙️ Tùy chỉnh theo yêu cầu</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">✅ Quản lý check-in</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">🎫 In thẻ lên máy bay</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">💺 Quản lý ghế ngồi</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">⏰ Cập nhật giờ bay / delay / cancel</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);background:rgba(76,201,240,0.05)"></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);background:rgba(76,201,240,0.05)"></td>
        </tr>
       </tbody>
      </table>
     </div>
     <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:12px;padding:16px;background:#041321;border-radius:12px;border:1px solid #4CC9F0">
      <div style="text-align:center">
       <div style="font-size:12px;color:#E5E7EB;margin-bottom:6px">
        Tổng tính năng
       </div>
       <div style="font-size:24px;font-weight:800;color:#FFD451">
        99
       </div>
      </div>
      <div style="text-align:center">
       <div style="font-size:12px;color:#E5E7EB;margin-bottom:6px">
        Tìm kiếm &amp; Đặt vé
       </div>
       <div style="font-size:24px;font-weight:800;color:#4CC9F0">
        33
       </div>
      </div>
      <div style="text-align:center">
       <div style="font-size:12px;color:#E5E7EB;margin-bottom:6px">
        Quản lý &amp; Dịch vụ
       </div>
       <div style="font-size:24px;font-weight:800;color:#10b981">
        33
       </div>
      </div>
      <div style="text-align:center">
       <div style="font-size:12px;color:#E5E7EB;margin-bottom:6px">
        Nâng cao &amp; Tích hợp
       </div>
       <div style="font-size:24px;font-weight:800;color:#3A86FF">
        33
       </div>
      </div>
     </div>
    </div><!-- PAYMENT SCHEDULE TABLE -->
    <div class="info-box" style="margin-top:32px">
     <h3 style="margin-top:0;color:#FFD451;font-weight:800;margin-bottom:20px">💰 Lịch thanh toán dự án AeroCore</h3>
     <div style="overflow-x:auto;margin-bottom:20px">
      <table style="width:100%;border-collapse:collapse;font-size:14px">
       <thead>
        <tr style="background:#041321;color:#FFD451;font-weight:700">
         <th style="padding:12px 8px;border:1px solid #4CC9F0;text-align:center">STT</th>
         <th style="padding:12px 8px;border:1px solid #4CC9F0;text-align:left">Nội dung thanh toán</th>
         <th style="padding:12px 8px;border:1px solid #4CC9F0;text-align:right">Số tiền (VND)</th>
         <th style="padding:12px 8px;border:1px solid #4CC9F0;text-align:right">Số dư còn lại (VND)</th>
         <th style="padding:12px 8px;border:1px solid #4CC9F0;text-align:center">Ngày chuyển</th>
         <th style="padding:12px 8px;border:1px solid #4CC9F0;text-align:center">Thứ</th>
         <th style="padding:12px 8px;border:1px solid #4CC9F0;text-align:center">Tình trạng</th>
         <th style="padding:12px 8px;border:1px solid #4CC9F0;text-align:left">Ghi chú nội bộ</th>
        </tr>
       </thead>
       <tbody style="color:#E5E7EB">
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">1</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT KHOI DONG DU AN</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.145.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">23.715.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">10/06/2024</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Hai</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đã xác nhận MB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">2</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT HA TANG CLOUD DATABASE</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.180.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">22.535.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">11/07/2024</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Năm</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đối chiếu VCB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">3</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT RUN NOW PACK TEST</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.205.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">21.330.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">13/08/2024</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Ba</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Hoàn tất kiểm tra cloud billing</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">4</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT GDS AMADEUS SABRE</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.565.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">19.765.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">13/09/2024</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Sáu</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đã xác nhận MB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">5</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT NDC BAMBOO VNA</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.615.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">18.150.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">16/10/2024</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Tư</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đối chiếu VCB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">6</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT KIEM THU GDS NDC</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.585.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">16.565.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">11/11/2024</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Hai</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Hoàn tất kiểm tra cloud billing</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">7</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT GDS NDC PRODUCTION</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.530.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">15.035.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">13/12/2024</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Sáu</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đã xác nhận MB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">8</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT AUTO TICKETING ENGINE</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.460.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">13.575.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">14/01/2025</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Ba</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đối chiếu VCB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">9</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT PAYMENT GATEWAY</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.480.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">12.095.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">13/02/2025</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Năm</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Hoàn tất kiểm tra cloud billing</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">10</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT FINALIZE BILLING</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.435.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">10.660.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">14/03/2025</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Sáu</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đã xác nhận MB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">11</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT AI PRICING</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.240.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">9.420.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">14/04/2025</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Hai</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đối chiếu VCB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">12</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT DEPLOY AI MODEL</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.210.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">8.210.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">15/05/2025</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Năm</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Hoàn tất kiểm tra cloud billing</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">13</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT DASHBOARD GRAFANA</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.075.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">7.135.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">13/06/2025</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Sáu</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đã xác nhận MB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">14</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT LOOK TO BOOK REPORT</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.035.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">6.100.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">14/07/2025</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Hai</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đối chiếu VCB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">15</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT SECURITY HARDENING</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">945.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">5.155.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">15/08/2025</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Sáu</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Hoàn tất kiểm tra cloud billing</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">16</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT CHUAN BI AUDIT</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">885.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">4.270.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">15/09/2025</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Hai</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đã xác nhận MB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">17</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT PORTAL DAILY</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">1.025.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#10b981;font-weight:600">3.245.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">15/10/2025</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Tư</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Đối chiếu VCB</td>
        </tr>
        <tr>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">18</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3)">TT GO LIVE DU AN</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#4CC9F0;font-weight:600">880.000.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:right;color:#ef4444;font-weight:600">-12.069.000</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">11/11/2025</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center">Ba</td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);text-align:center"><span style="background:rgba(16,185,129,0.2);color:#10b981;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700">Đã TT</span></td>
         <td style="padding:10px 8px;border:1px solid rgba(76,201,240,0.3);font-size:12px">Hoàn tất kiểm tra cloud billing</td>
        </tr>
       </tbody>
      </table>
     </div>
     <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:16px;padding:16px;background:#041321;border-radius:12px;border:1px solid #4CC9F0">
      <div style="text-align:center">
       <div style="font-size:12px;color:#E5E7EB;margin-bottom:6px">
        Tổng thanh toán
       </div>
       <div style="font-size:20px;font-weight:800;color:#4CC9F0">
        22.460 tỷ
       </div>
      </div>
      <div style="text-align:center">
       <div style="font-size:12px;color:#E5E7EB;margin-bottom:6px">
        Số dư ban đầu
       </div>
       <div style="font-size:20px;font-weight:800;color:#10b981">
        24.860 tỷ
       </div>
      </div>
      <div style="text-align:center">
       <div style="font-size:12px;color:#E5E7EB;margin-bottom:6px">
        Số dư cuối
       </div>
       <div style="font-size:20px;font-weight:800;color:#ef4444">
        -12 triệu
       </div>
      </div>
      <div style="text-align:center">
       <div style="font-size:12px;color:#E5E7EB;margin-bottom:6px">
        Số đợt TT
       </div>
       <div style="font-size:20px;font-weight:800;color:#FFD451">
        18 đợt
       </div>
      </div>
     </div>
    </div>
   </div>
  </div><!-- END PAGES WRAPPER -->
  <script>
// ===== GLOBAL STATE =====
let currentPage = 'search';
let selectedFlight = null;
let passengers = [];
let currentUser = null;
let allBookings = [];

// ===== DATA SDK SETUP =====
const dataHandler = {
  onDataChanged(data) {
    allBookings = data;
    updateDashboardFromBookings();
    
    if (currentPage === 'mybookings') {
      renderMyBookings();
    }
  }
};

async function initDataSDK() {
  if (!window.dataSdk) {
    console.error('Data SDK not available');
    return;
  }
  
  const result = await window.dataSdk.init(dataHandler);
  if (!result.isOk) {
    console.error('Failed to initialize Data SDK:', result.error);
  }
}

// ===== REALTIME CLOCK =====
function updateRealtimeClock() {
  const now = new Date();
  
  const hours = String(now.getHours()).padStart(2, '0');
  const minutes = String(now.getMinutes()).padStart(2, '0');
  const seconds = String(now.getSeconds()).padStart(2, '0');
  
  const day = String(now.getDate()).padStart(2, '0');
  const month = String(now.getMonth() + 1).padStart(2, '0');
  const year = now.getFullYear();
  
  const clockEl = document.getElementById('clockDisplay');
  const dateEl = document.getElementById('dateDisplay');
  
  if (clockEl) {
    clockEl.textContent = `${hours}:${minutes}:${seconds}`;
  }
  
  if (dateEl) {
    dateEl.textContent = `${day}/${month}/${year}`;
  }
}

// ===== NAVIGATION =====
const pageOrder = ['login', 'search', 'passenger', 'payment', 'mybookings', 'dashboard'];

function navigateTo(page) {
  if (!currentUser && ['passenger', 'payment', 'mybookings'].includes(page)) {
    showLoginModal();
    return;
  }
  
  const oldPage = currentPage;
  const oldIndex = pageOrder.indexOf(oldPage);
  const newIndex = pageOrder.indexOf(page);
  
  const oldPageEl = document.getElementById('page' + capitalize(oldPage));
  const newPageEl = document.getElementById('page' + capitalize(page));
  
  if (!newPageEl) return;
  
  const direction = newIndex > oldIndex ? 'left' : 'right';
  
  newPageEl.classList.remove('hidden');
  newPageEl.classList.remove('active');
  newPageEl.classList.add(direction === 'left' ? 'slide-in-right' : 'slide-in-left');
  
  void newPageEl.offsetWidth;
  
  if (oldPageEl) {
    oldPageEl.classList.remove('active');
    oldPageEl.classList.add(direction === 'left' ? 'slide-out-left' : 'slide-out-right');
  }
  
  newPageEl.classList.remove('slide-in-left', 'slide-in-right');
  newPageEl.classList.add('active');
  
  setTimeout(() => {
    if (oldPageEl) {
      oldPageEl.classList.add('hidden');
      oldPageEl.classList.remove('slide-out-left', 'slide-out-right');
    }
  }, 400);
  
  document.querySelectorAll('.nav-link').forEach(link => {
    link.classList.remove('active');
    if (link.textContent.toLowerCase().includes(page.replace('page', ''))) {
      link.classList.add('active');
    }
  });
  
  currentPage = page;
  window.scrollTo(0, 0);
  
  if (page === 'passenger') generatePassengerForms();
  else if (page === 'payment') updatePaymentTotal();
  else if (page === 'mybookings') loadMyBookings();
  else if (page === 'dashboard') {
    updateDashboardMetrics();
    setTimeout(() => {
      if (window.mermaid) {
        mermaid.init(undefined, document.querySelectorAll('.mermaid'));
      }
    }, 100);
  }
}

function capitalize(str) {
  return str.charAt(0).toUpperCase() + str.slice(1);
}

// ===== UTILITY FUNCTIONS =====
function escapeHtml(str) {
  const div = document.createElement('div');
  div.textContent = str;
  return div.innerHTML;
}

function showMessage(elementId, text, type) {
  const el = document.getElementById(elementId);
  if (!el) return;
  el.textContent = text;
  el.className = 'message ' + type;
}

// ===== TOAST NOTIFICATIONS =====
function showToast(title, message, type = 'info', duration = 4000) {
  let container = document.getElementById('toastContainer');
  
  if (!container) {
    container = document.createElement('div');
    container.id = 'toastContainer';
    container.className = 'toast-container';
    document.body.appendChild(container);
  }
  
  const icons = {
    success: '✓',
    error: '✗',
    info: 'ℹ',
    warning: '⚠'
  };
  
  const colors = {
    success: '#10b981',
    error: '#ef4444',
    info: '#4CC9F0',
    warning: '#f59e0b'
  };
  
  const toast = document.createElement('div');
  toast.className = `toast toast-${type}`;
  
  toast.innerHTML = `
    <div class="toast-icon" style="color:${colors[type]}">${icons[type]}</div>
    <div class="toast-content">
      <div class="toast-title" style="color:${colors[type]}">${escapeHtml(title)}</div>
      <div class="toast-message">${escapeHtml(message)}</div>
    </div>
    <button class="toast-close">×</button>
  `;
  
  const closeBtn = toast.querySelector('.toast-close');
  closeBtn.onclick = () => removeToast(toast);
  
  container.appendChild(toast);
  
  if (duration > 0) {
    setTimeout(() => removeToast(toast), duration);
  }
  
  return toast;
}

function removeToast(toast) {
  toast.style.animation = 'slideOutRight 0.3s ease';
  setTimeout(() => {
    if (toast.parentNode) {
      toast.parentNode.removeChild(toast);
    }
  }, 300);
}

// ===== LOGIN =====
function showLoginModal() {
  const modal = document.createElement('div');
  modal.className = 'modal-overlay';
  modal.innerHTML = `
    <div class="modal-content">
      <div class="modal-title">🔐 Đăng nhập để tiếp tục</div>
      <p style="color:#E5E7EB;margin-bottom:20px">Vui lòng đăng nhập để đặt vé và quản lý booking</p>
      
      <div class="form-group">
        <label class="form-label" for="modalEmail">Email</label>
        <input class="form-input" id="modalEmail" type="email" placeholder="your@email.com">
      </div>
      
      <div class="form-group">
        <label class="form-label" for="modalName">Họ tên</label>
        <input class="form-input" id="modalName" placeholder="Nguyễn Văn A">
      </div>
      
      <div class="modal-buttons">
        <button class="btn btn-secondary" style="flex:1" onclick="this.closest('.modal-overlay').remove()">Hủy</button>
        <button class="btn btn-primary" style="flex:1" onclick="doLoginFromModal()">Đăng nhập</button>
      </div>
    </div>
  `;
  document.body.appendChild(modal);
}

function doLogin() {
  const email = document.getElementById('loginEmail').value.trim();
  const name = document.getElementById('loginName').value.trim();
  
  if (!email || !name) {
    showMessage('loginMessage', '⚠️ Vui lòng nhập đầy đủ thông tin', 'error');
    return;
  }
  
  if (!email.includes('@')) {
    showMessage('loginMessage', '⚠️ Email không hợp lệ', 'error');
    return;
  }
  
  currentUser = { email, name };
  localStorage.setItem('currentUser', JSON.stringify(currentUser));
  
  updateUserUI();
  showMessage('loginMessage', '✓ Đăng nhập thành công!', 'success');
  showToast('Chào mừng!', `Đăng nhập thành công với ${email}`, 'success');
  
  setTimeout(() => {
    navigateTo('search');
  }, 1000);
}

function doLoginFromModal() {
  const email = document.getElementById('modalEmail').value.trim();
  const name = document.getElementById('modalName').value.trim();
  
  if (!email || !name || !email.includes('@')) {
    return;
  }
  
  currentUser = { email, name };
  localStorage.setItem('currentUser', JSON.stringify(currentUser));
  
  updateUserUI();
  
  document.querySelector('.modal-overlay').remove();
  
  if (selectedFlight) {
    navigateTo('passenger');
  }
}

function logout() {
  const userEmail = currentUser ? currentUser.email : '';
  currentUser = null;
  localStorage.removeItem('currentUser');
  updateUserUI();
  showToast('Đã đăng xuất', `Tạm biệt ${userEmail}!`, 'info');
  navigateTo('search');
}

function updateUserUI() {
  const userInfo = document.getElementById('userInfo');
  const userEmail = document.getElementById('userEmail');
  
  if (currentUser) {
    userInfo.style.display = 'flex';
    userEmail.textContent = currentUser.email;
  } else {
    userInfo.style.display = 'none';
  }
}

// ===== SEARCH PAGE =====
function doSearch() {
  const from = document.getElementById('searchFrom').value.trim().toUpperCase();
  const to = document.getElementById('searchTo').value.trim().toUpperCase();
  const date = document.getElementById('searchDate').value;
  
  if (!from || !to || !date) {
    showMessage('searchMessage', '⚠️ Vui lòng điền đầy đủ thông tin', 'error');
    return;
  }
  
  showMessage('searchMessage', '🔍 Đang tìm kiếm chuyến bay...', 'info');
  
  setTimeout(() => {
    const flights = generateFlights(from, to, date);
    displaySearchResults(flights);
    showMessage('searchMessage', `✓ Tìm thấy ${flights.length} chuyến bay!`, 'success');
  }, 800);
}

function generateFlights(from, to, date) {
  const airlines = [
    { code: 'VN', name: 'Vietnam Airlines', type: 'NDC' },
    { code: 'VJ', name: 'Vietjet Air', type: 'LCC' },
    { code: 'QH', name: 'Bamboo Airways', type: 'NDC' },
    { code: 'BL', name: 'Pacific Airlines', type: 'LCC' },
    { code: 'AK', name: 'AirAsia', type: 'LCC' }
  ];
  
  const flights = [];
  
  for (let i = 0; i < 5; i++) {
    const airline = airlines[i];
    
    const departHour = 6 + i * 2;
    const duration = 120 + Math.floor(Math.random() * 60);
    const arriveHour = departHour + Math.floor(duration / 60);
    const arriveMin = duration % 60;
    
    flights.push({
      id: 'FL' + Math.random().toString(36).substring(2, 8).toUpperCase(),
      airline: airline.name,
      airline_code: airline.code,
      airline_type: airline.type,
      flight_number: airline.code + (200 + i),
      from, to, date,
      depart: `${String(departHour).padStart(2, '0')}:00`,
      arrive: `${String(arriveHour).padStart(2, '0')}:${String(arriveMin).padStart(2, '0')}`,
      duration: `${Math.floor(duration / 60)}h ${duration % 60}m`,
      price: 1500000 + Math.floor(Math.random() * 2000000),
      aircraft: 'A321'
    });
  }
  
  return flights;
}

function displaySearchResults(flights) {
  const container = document.getElementById('searchResults');
  if (!container) return;
  
  let html = '';
  flights.forEach(flight => {
    const airlineType = flight.airline_type || 'GDS';
    const typeBadgeColor = airlineType === 'NDC' ? '#4CC9F0' : airlineType === 'LCC' ? '#FFD451' : '#3A86FF';
    const typeBadge = `<span style="background:${typeBadgeColor};color:#041321;padding:4px 8px;border-radius:6px;font-size:11px;font-weight:700;margin-left:8px">${airlineType}</span>`;
    
    html += `
      <div class="result-card" onclick='selectFlight(${JSON.stringify(flight).replace(/'/g, "&#39;")})'>
        <div class="flight-header">
          <div class="airline-name">
            ${escapeHtml(flight.airline)}
            ${typeBadge}
          </div>
          <div class="flight-price">${flight.price.toLocaleString('vi-VN')} ₫</div>
        </div>
        
        <div class="flight-route">
          <div class="flight-time">
            <div class="time">${flight.depart}</div>
            <div class="airport">${escapeHtml(flight.from)}</div>
          </div>
          
          <div class="flight-duration">
            <div class="duration">${flight.duration}</div>
            <div style="font-size:12px;color:#E5E7EB;margin-top:4px">Direct</div>
          </div>
          
          <div class="flight-time">
            <div class="time">${flight.arrive}</div>
            <div class="airport">${escapeHtml(flight.to)}</div>
          </div>
        </div>
        
        <div class="flight-details">
          <span>✈️ ${escapeHtml(flight.flight_number)}</span>
          <span>🛩️ ${escapeHtml(flight.aircraft)}</span>
          <span>✓ Available</span>
        </div>
      </div>
    `;
  });
  
  container.innerHTML = html;
}

function selectFlight(flight) {
  if (!currentUser) {
    selectedFlight = flight;
    showLoginModal();
    return;
  }
  
  selectedFlight = flight;
  navigateTo('passenger');
}

// ===== PASSENGER PAGE =====
function generatePassengerForms() {
  const container = document.getElementById('passengerForms');
  if (!container) return;
  
  if (passengers.length === 0) {
    passengers = [{ name: '', dob: '', gender: 'Male', doc: '' }];
  }
  
  let html = '';
  passengers.forEach((pax, i) => {
    html += `
      <div class="passenger-box">
        <h3 style="margin-top:0;color:#FFD451;font-weight:800">Hành khách ${i + 1}</h3>
        
        <div class="form-group">
          <label class="form-label" for="paxName${i}">Họ tên</label>
          <input class="form-input" id="paxName${i}" placeholder="Nguyễn Văn A" value="${escapeHtml(pax.name || '')}">
        </div>
        
        <div class="form-grid">
          <div class="form-group">
            <label class="form-label" for="paxDob${i}">Ngày sinh</label>
            <input class="form-input" id="paxDob${i}" type="date" value="${pax.dob || ''}">
          </div>
          <div class="form-group">
            <label class="form-label" for="paxGender${i}">Giới tính</label>
            <select class="form-input" id="paxGender${i}">
              <option ${pax.gender === 'Male' ? 'selected' : ''}>Male</option>
              <option ${pax.gender === 'Female' ? 'selected' : ''}>Female</option>
            </select>
          </div>
        </div>
        
        <div class="form-group">
          <label class="form-label" for="paxDoc${i}">CMND / Hộ chiếu</label>
          <input class="form-input" id="paxDoc${i}" placeholder="012345678" value="${escapeHtml(pax.doc || '')}">
        </div>
      </div>
    `;
  });
  
  container.innerHTML = html;
}

function collectPassengerData() {
  const data = [];
  passengers.forEach((pax, i) => {
    const nameEl = document.getElementById(`paxName${i}`);
    const dobEl = document.getElementById(`paxDob${i}`);
    const genderEl = document.getElementById(`paxGender${i}`);
    const docEl = document.getElementById(`paxDoc${i}`);
    
    if (nameEl && dobEl && genderEl && docEl) {
      data.push({
        name: nameEl.value.trim(),
        dob: dobEl.value,
        gender: genderEl.value,
        doc: docEl.value.trim()
      });
    }
  });
  return data;
}

function addPassenger() {
  passengers = collectPassengerData();
  passengers.push({ name: '', dob: '', gender: 'Male', doc: '' });
  generatePassengerForms();
  showMessage('passengerMessage', `✓ Đã thêm hành khách ${passengers.length}`, 'success');
  setTimeout(() => showMessage('passengerMessage', '', ''), 2000);
}

function removePassenger() {
  if (passengers.length <= 1) {
    showMessage('passengerMessage', '⚠️ Phải có ít nhất 1 h��nh khách', 'error');
    return;
  }
  passengers = collectPassengerData();
  passengers.pop();
  generatePassengerForms();
  showMessage('passengerMessage', `✓ Đã xóa hành khách`, 'success');
  setTimeout(() => showMessage('passengerMessage', '', ''), 2000);
}

function goToPayment() {
  passengers = collectPassengerData();
  for (let i = 0; i < passengers.length; i++) {
    if (!passengers[i].name) {
      showMessage('passengerMessage', `⚠️ Hành khách ${i + 1}: Vui lòng nhập họ tên`, 'error');
      return;
    }
  }
  navigateTo('payment');
}

// ===== PAYMENT PAGE =====
function updatePaymentTotal() {
  const totalEl = document.getElementById('paymentTotal');
  const detailsEl = document.getElementById('paymentDetails');
  const emailEl = document.getElementById('confirmEmail');
  
  if (!totalEl || !selectedFlight) return;
  
  const total = selectedFlight.price * passengers.length;
  totalEl.textContent = total.toLocaleString('vi-VN') + ' ₫';
  
  if (detailsEl) {
    detailsEl.textContent = `${selectedFlight.price.toLocaleString('vi-VN')} ₫ × ${passengers.length} hành khách`;
  }
  
  if (emailEl && currentUser) {
    emailEl.value = currentUser.email;
  }
}

async function submitPayment() {
  const emailEl = document.getElementById('confirmEmail');
  const email = emailEl ? emailEl.value.trim() : '';
  
  if (!email || !email.includes('@')) {
    showMessage('paymentMessage', '⚠️ Vui lòng nhập email hợp lệ', 'error');
    return;
  }
  
  const btn = document.getElementById('paymentSubmitBtn');
  btn.disabled = true;
  btn.textContent = 'Đang xử lý...';
  
  showMessage('paymentMessage', '💳 Đang xử lý đặt vé...', 'info');
  
  if (allBookings.length >= 999) {
    showMessage('paymentMessage', '⚠️ Đã đạt giới hạn 999 booking. Vui lòng xóa booking cũ.', 'error');
    btn.disabled = false;
    btn.textContent = 'Xác nhận đặt vé';
    return;
  }
  
  const pnr = 'PNR' + Math.random().toString(36).substring(2, 8).toUpperCase();
  const bookingId = 'BK' + Date.now() + Math.random().toString(36).substring(2, 6).toUpperCase();
  
  const ticketNumbers = passengers.map(() => 
    'TCK' + Math.random().toString(36).substring(2, 10).toUpperCase()
  );
  
  const bookingRecord = {
    booking_id: bookingId,
    pnr: pnr,
    user_email: email,
    flight_id: selectedFlight.id,
    airline: selectedFlight.airline,
    airline_code: selectedFlight.airline_code,
    flight_number: selectedFlight.flight_number,
    from: selectedFlight.from,
    to: selectedFlight.to,
    date: selectedFlight.date,
    depart: selectedFlight.depart,
    arrive: selectedFlight.arrive,
    duration: selectedFlight.duration,
    price: selectedFlight.price,
    total_price: selectedFlight.price * passengers.length,
    passengers: JSON.stringify(passengers),
    status: 'confirmed',
    created_at: new Date().toISOString(),
    checked_in: false,
    ticket_numbers: JSON.stringify(ticketNumbers)
  };
  
  const result = await window.dataSdk.create(bookingRecord);
  
  btn.disabled = false;
  btn.textContent = 'Xác nhận đặt vé';
  
  if (result.isOk) {
    showMessage('paymentMessage', '✓ Đặt vé thành công!', 'success');
    showToast('Đặt vé thành công!', `PNR: ${pnr} • ${passengers.length} hành khách • ${selectedFlight.from} → ${selectedFlight.to}`, 'success', 5000);
    setTimeout(() => {
      navigateTo('mybookings');
    }, 1500);
  } else {
    showMessage('paymentMessage', '⚠️ Có lỗi xảy ra. Vui lòng thử lại.', 'error');
    showToast('Lỗi đặt vé', 'Không thể hoàn tất đặt vé. Vui lòng thử lại.', 'error');
  }
}

// ===== MY BOOKINGS PAGE =====
function loadMyBookings() {
  const loadingEl = document.getElementById('loadingBookings');
  const listEl = document.getElementById('bookingsList');
  const noBookingsEl = document.getElementById('noBookings');
  
  if (loadingEl) loadingEl.style.display = 'block';
  if (listEl) listEl.innerHTML = '';
  if (noBookingsEl) noBookingsEl.style.display = 'none';
  
  setTimeout(() => {
    if (loadingEl) loadingEl.style.display = 'none';
    renderMyBookings();
  }, 500);
}

function renderMyBookings() {
  const listEl = document.getElementById('bookingsList');
  const noBookingsEl = document.getElementById('noBookings');
  
  if (!listEl || !noBookingsEl) return;
  
  const userBookings = currentUser 
    ? allBookings.filter(b => b.user_email === currentUser.email)
    : [];
  
  if (userBookings.length === 0) {
    listEl.innerHTML = '';
    noBookingsEl.style.display = 'block';
    return;
  }
  
  noBookingsEl.style.display = 'none';
  
  let html = '';
  userBookings.forEach(booking => {
    const statusClass = booking.status === 'confirmed' ? 'status-confirmed' : 
                       booking.status === 'cancelled' ? 'status-cancelled' : 
                       'status-checked-in';
    const statusText = booking.status === 'confirmed' ? 'Confirmed' : 
                      booking.status === 'cancelled' ? 'Cancelled' : 
                      'Checked In';
    
    const passengers = JSON.parse(booking.passengers || '[]');
    
    html += `
      <div class="result-card" style="cursor:default">
        <div class="flight-header">
          <div>
            <div class="airline-name">${escapeHtml(booking.airline)}</div>
            <div style="font-size:14px;color:#E5E7EB;margin-top:4px">PNR: ${booking.pnr}</div>
          </div>
          <div>
            <div class="flight-price">${booking.total_price.toLocaleString('vi-VN')} ��</div>
            <span class="status-badge ${statusClass}" style="margin-top:8px;display:inline-block">${statusText}</span>
          </div>
        </div>
        
        <div class="flight-route">
          <div class="flight-time">
            <div class="time">${booking.depart}</div>
            <div class="airport">${escapeHtml(booking.from)}</div>
          </div>
          
          <div class="flight-duration">
            <div class="duration">${booking.duration}</div>
            <div style="font-size:12px;color:#E5E7EB;margin-top:4px">${booking.date}</div>
          </div>
          
          <div class="flight-time">
            <div class="time">${booking.arrive}</div>
            <div class="airport">${escapeHtml(booking.to)}</div>
          </div>
        </div>
        
        <div class="flight-details">
          <span>✈️ ${escapeHtml(booking.flight_number)}</span>
          <span>👥 ${passengers.length} hành khách</span>
          <span>📅 ${new Date(booking.created_at).toLocaleDateString('vi-VN')}</span>
        </div>
        
        <div style="display:flex;gap:12px;margin-top:16px;padding-top:16px;border-top:1px solid rgba(76,201,240,0.3)">
          ${booking.status === 'confirmed' && !booking.checked_in ? `
            <button class="btn btn-success" style="flex:1;padding:10px" onclick="checkIn('${booking.__backendId}')">✓ Check-in</button>
          ` : ''}
          ${booking.status === 'confirmed' ? `
            <button class="btn btn-danger" style="flex:1;padding:10px" onclick="cancelBooking('${booking.__backendId}')">✗ Hủy vé</button>
          ` : ''}
          <button class="btn btn-secondary" style="flex:1;padding:10px" onclick="viewTickets('${booking.__backendId}')">🎫 Xem vé</button>
        </div>
      </div>
    `;
  });
  
  listEl.innerHTML = html;
}

async function checkIn(backendId) {
  const booking = allBookings.find(b => b.__backendId === backendId);
  if (!booking) return;
  
  const modal = document.createElement('div');
  modal.className = 'modal-overlay';
  modal.innerHTML = `
    <div class="modal-content">
      <div class="modal-title">✈️ Check-in</div>
      <p style="color:#E5E7EB;margin-bottom:20px">Xác nhận check-in cho chuyến bay ${booking.flight_number}?</p>
      <div class="modal-buttons">
        <button class="btn btn-secondary" style="flex:1" onclick="this.closest('.modal-overlay').remove()">Hủy</button>
        <button class="btn btn-success" style="flex:1" onclick="confirmCheckIn('${backendId}')">Xác nhận</button>
      </div>
    </div>
  `;
  document.body.appendChild(modal);
}

async function confirmCheckIn(backendId) {
  const booking = allBookings.find(b => b.__backendId === backendId);
  if (!booking) return;
  
  booking.checked_in = true;
  booking.status = 'checked_in';
  
  const result = await window.dataSdk.update(booking);
  
  document.querySelector('.modal-overlay').remove();
  
  if (result.isOk) {
    showToast('Check-in thành công!', `Chuyến bay ${booking.flight_number} • ${booking.from} → ${booking.to}`, 'success');
  } else {
    showToast('Lỗi check-in', 'Không thể check-in. Vui lòng thử lại.', 'error');
  }
}

async function cancelBooking(backendId) {
  const booking = allBookings.find(b => b.__backendId === backendId);
  if (!booking) return;
  
  const modal = document.createElement('div');
  modal.className = 'modal-overlay';
  modal.innerHTML = `
    <div class="modal-content">
      <div class="modal-title">⚠️ Hủy vé</div>
      <p style="color:#E5E7EB;margin-bottom:20px">Bạn có chắc muốn hủy vé cho chuyến bay ${booking.flight_number}?</p>
      <p style="color:#fca5a5;font-size:13px;margin-bottom:20px">Hành động này không thể hoàn tác.</p>
      <div class="modal-buttons">
        <button class="btn btn-secondary" style="flex:1" onclick="this.closest('.modal-overlay').remove()">Không</button>
        <button class="btn btn-danger" style="flex:1" onclick="confirmCancel('${backendId}')">Xác nhận hủy</button>
      </div>
    </div>
  `;
  document.body.appendChild(modal);
}

async function confirmCancel(backendId) {
  const booking = allBookings.find(b => b.__backendId === backendId);
  if (!booking) return;
  
  booking.status = 'cancelled';
  
  const result = await window.dataSdk.update(booking);
  
  document.querySelector('.modal-overlay').remove();
  
  if (result.isOk) {
    showToast('Đã hủy vé', `PNR: ${booking.pnr} • ${booking.flight_number}`, 'warning');
  } else {
    showToast('Lỗi hủy vé', 'Không thể hủy vé. Vui lòng thử lại.', 'error');
  }
}

function viewTickets(backendId) {
  const booking = allBookings.find(b => b.__backendId === backendId);
  if (!booking) return;
  
  const passengers = JSON.parse(booking.passengers || '[]');
  const ticketNumbers = JSON.parse(booking.ticket_numbers || '[]');
  
  let ticketsHtml = '';
  passengers.forEach((p, i) => {
    const qrData = encodeURIComponent(`${booking.pnr}-${ticketNumbers[i]}-${p.name}`);
    ticketsHtml += `
      <div style="background:#041321;padding:20px;border-radius:12px;margin-bottom:16px;border:2px solid #4CC9F0">
        <h4 style="color:#FFD451;margin-top:0;margin-bottom:12px">${escapeHtml(p.name)}</h4>
        <div style="font-size:13px;color:#E5E7EB;margin-bottom:8px">
          <strong>Ticket:</strong> ${ticketNumbers[i]}<br>
          <strong>Flight:</strong> ${booking.flight_number}<br>
          <strong>Route:</strong> ${booking.from} → ${booking.to}<br>
          <strong>Date:</strong> ${booking.date} ${booking.depart}
        </div>
        <div style="text-align:center;margin-top:12px">
          <img src="https://api.qrserver.com/v1/create-qr-code/?size=120x120&data=${qrData}" style="width:120px;height:120px;border:2px solid #FFD451;border-radius:8px;background:white;padding:4px" alt="QR Code">
        </div>
      </div>
    `;
  });
  
  const modal = document.createElement('div');
  modal.className = 'modal-overlay';
  modal.innerHTML = `
    <div class="modal-content" style="max-width:600px;max-height:80%;overflow-y:auto">
      <div class="modal-title">🎫 Vé điện tử</div>
      <div style="margin-bottom:20px">
        <div style="font-size:24px;font-weight:800;color:#FFD451;text-align:center;margin-bottom:8px">${booking.pnr}</div>
        <div style="text-align:center;color:#E5E7EB;font-size:14px">${booking.airline} • ${booking.flight_number}</div>
      </div>
      ${ticketsHtml}
      <button class="btn btn-primary" style="width:100%" onclick="this.closest('.modal-overlay').remove()">Đóng</button>
    </div>
  `;
  document.body.appendChild(modal);
}

// ===== DASHBOARD =====
function updateDashboardFromBookings() {
  const totalBookings = allBookings.length;
  const totalRevenue = allBookings.reduce((sum, b) => sum + (b.total_price || 0), 0);
  
  const metricBookingsEl = document.getElementById('metricBookings');
  const metricRevenueEl = document.getElementById('metricRevenue');
  
  if (metricBookingsEl) {
    metricBookingsEl.textContent = totalBookings.toLocaleString();
  }
  
  if (metricRevenueEl) {
    metricRevenueEl.textContent = '$' + (totalRevenue / 23000).toFixed(1) + 'K';
  }
}

function updateDashboardMetrics() {
  updateDashboardFromBookings();
}

// ===== INITIALIZATION =====
window.addEventListener('DOMContentLoaded', async () => {
  // Initialize Mermaid
  if (window.mermaid) {
    mermaid.initialize({ 
      startOnLoad: true,
      theme: 'dark',
      themeVariables: {
        primaryColor: '#4CC9F0',
        primaryTextColor: '#FFFFFF',
        primaryBorderColor: '#FFD451',
        lineColor: '#4CC9F0',
        secondaryColor: '#0B2840',
        tertiaryColor: '#041321'
      }
    });
  }
  
  // Initialize Data SDK
  await initDataSDK();
  
  // Start realtime clock
  updateRealtimeClock();
  setInterval(updateRealtimeClock, 1000);
  
  // Check saved user
  const savedUser = localStorage.getItem('currentUser');
  if (savedUser) {
    currentUser = JSON.parse(savedUser);
    updateUserUI();
  }
  
  // Set default date
  const tomorrow = new Date();
  tomorrow.setDate(tomorrow.getDate() + 1);
  const dateInput = document.getElementById('searchDate');
  if (dateInput) {
    dateInput.value = tomorrow.toISOString().split('T')[0];
  }
});
</script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9a38c5ba340d20bb',t:'MTc2Mzk4NTkwNC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
