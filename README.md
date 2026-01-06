<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
  <title>PAYEER TECH</title>

  <!-- Telegram WebApp -->
  <script src="https://telegram.org/js/telegram-web-app.js"></script>

  <!-- Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">

  <style>
    body{margin:0;background:#000;font-family:Segoe UI,sans-serif;color:#fff}
    .header{padding:15px;background:#111;text-align:center;font-weight:bold;color:#e53935}
    .profile{display:flex;align-items:center;background:#111;padding:15px;margin:15px;border-radius:15px}
    .profile img{width:55px;height:55px;border-radius:50%;margin-right:15px;border:2px solid #e53935}
    .profile-info small{color:#aaa}
    .balance{background:linear-gradient(135deg,#e53935,#43a047);margin:15px;padding:20px;border-radius:18px;text-align:center}
    .balance h2{margin:5px 0;font-size:26px}
    .message{background:#111;margin:15px;padding:12px;border-left:4px solid #e53935;border-radius:10px;font-size:14px}
    .content{padding:15px;padding-bottom:80px}
    .card{background:#111;padding:15px;border-radius:15px;margin-bottom:15px}
    button{width:100%;padding:12px;border:none;border-radius:10px;background:#e53935;color:#fff;font-size:15px;margin-top:10px}
    input{width:100%;padding:10px;border-radius:8px;border:none;margin-top:8px}
    .nav{position:fixed;bottom:0;width:100%;background:#111;display:flex;justify-content:space-around;padding:10px 0;border-top:1px solid #222}
    .nav i{font-size:20px;color:#aaa}
    .nav i.active{color:#e53935}
  </style>
</head>
<body>

<div class="header">PAYEER TECH</div>

<!-- PROFILE -->
<div class="profile">
  <img id="profilePic" src="https://i.pravatar.cc/150" />
  <div class="profile-info">
    <strong>User ID: <span id="uid">---</span></strong><br>
    <small>Total Earned: ₦<span id="earned">0</span></small>
  </div>
</div>

<!-- BALANCE -->
<div class="balance">
  <small>Available Balance</small>
  <h2>₦<span id="balance">0</span></h2>
</div>

<!-- ADMIN MESSAGE -->
<div class="message" id="announcement">📢 Loading announcement...</div>

<!-- CONTENT -->
<div class="content">

  <div class="card">
    <h4>🎥 Available Tasks</h4>
    <p>Watch video & submit proof</p>
    <button onclick="submitTask()">Submit Task</button>
  </div>

  <div class="card">
    <h4>🤝 Referral Program</h4>
    <p>Invite friends & earn ₦1000</p>
    <input id="refLink" readonly />
    <button onclick="copyRef()">Copy Referral Link</button>
  </div>

  <div class="card">
    <h4>🏦 Withdraw Earnings</h4>
    <p>Minimum ₦5000 • Subscription ₦2000</p>
    <button onclick="requestWithdrawal()">Request Withdrawal</button>
  </div>

</div>

<!-- NAV -->
<div class="nav">
  <i class="fa fa-home active"></i>
  <i class="fa fa-tasks"></i>
  <i class="fa fa-users"></i>
  <i class="fa fa-wallet"></i>
</div>

<script>
const BACKEND = 'https://your-backend.com'; // CHANGE THIS
const tg = window.Telegram.WebApp;
tg.ready();

const tgUser = tg.initDataUnsafe.user;

if (tgUser) {
  document.getElementById('uid').innerText = tgUser.id;
  if (tgUser.photo_url) {
    document.getElementById('profilePic').src = tgUser.photo_url;
  }
  document.getElementById('refLink').value = `https://t.me/YourBot?start=REF_${tgUser.id}`;
}

async function loadUser() {
  const res = await fetch(`${BACKEND}/api/user`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ telegramId: tgUser.id })
  });

  const data = await res.json();
  document.getElementById('balance').innerText = data.balance;
  document.getElementById('earned').innerText = data.totalEarned;
}

async function loadAnnouncement() {
  const res = await fetch(`${BACKEND}/api/announcement`);
  const data = await res.json();
  document.getElementById('announcement').innerText = '📢 ' + data.message;
}

function copyRef() {
  navigator.clipboard.writeText(document.getElementById('refLink').value);
  alert('Referral link copied');
}

function submitTask() {
  alert('Task submitted for admin approval');
}

function requestWithdrawal() {
  alert('Withdrawal request sent to admin');
}

loadUser();
loadAnnouncement();
</script>

</body>
</html>
