<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PAYEER TECH</title>

  <!-- Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" />

  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', Arial, sans-serif;
      background: #000;
      color: #fff;
    }

    header {
      background: #0d0d0d;
      padding: 16px;
      text-align: center;
      font-size: 22px;
      font-weight: 700;
      color: #e53935;
      letter-spacing: 1px;
    }

    .balance {
      margin: 15px;
      padding: 20px;
      border-radius: 18px;
      background: linear-gradient(135deg, #2e7d32, #c62828);
      box-shadow: 0 8px 25px rgba(0,0,0,0.6);
      text-align: center;
    }

    .balance h2 {
      margin: 0;
      font-size: 15px;
      opacity: 0.9;
    }

    .balance p {
      font-size: 34px;
      margin-top: 10px;
      font-weight: bold;
    }

    .container {
      padding: 15px;
      padding-bottom: 110px;
    }

    .card {
      background: #111;
      border-radius: 16px;
      padding: 15px;
      margin-bottom: 15px;
      box-shadow: 0 6px 18px rgba(0,0,0,0.6);
    }

    h3 {
      margin-top: 0;
      color: #4caf50;
      font-size: 16px;
    }

    .leaderboard li {
      margin-bottom: 6px;
    }

    .notice {
      background: linear-gradient(135deg, #1c1c1c, #111);
      border-left: 4px solid #e53935;
    }

    input {
      width: 100%;
      padding: 12px;
      border-radius: 10px;
      border: none;
      background: #1b1b1b;
      color: #fff;
      margin-top: 10px;
    }

    button {
      width: 100%;
      padding: 14px;
      margin-top: 12px;
      border: none;
      border-radius: 12px;
      background: linear-gradient(135deg, #e53935, #b71c1c);
      color: #fff;
      font-size: 15px;
      font-weight: bold;
    }

    /* Floating bottom navigation */
    .menu {
      position: fixed;
      bottom: 15px;
      left: 50%;
      transform: translateX(-50%);
      width: 92%;
      background: #111;
      border-radius: 25px;
      display: flex;
      justify-content: space-around;
      padding: 12px 0;
      box-shadow: 0 8px 25px rgba(0,0,0,0.7);
    }

    .menu button {
      background: none;
      border: none;
      color: #aaa;
      font-size: 12px;
    }

    .menu i {
      display: block;
      font-size: 18px;
      margin-bottom: 4px;
    }

    .menu .active {
      color: #e53935;
    }

    .page { display: none; }
    .page.active { display: block; }
  </style>
</head>
<body>

<header>PAYEER TECH</header>

<!-- HOME -->
<div id="home" class="page active">
  <div class="balance">
    <h2>Available Balance</h2>
    <p>₦<span id="balance">0</span></p>
  </div>

  <div class="container">
    <div class="card">
      <h3><i class="fa-solid fa-trophy"></i> Leaderboard</h3>
      <ol class="leaderboard">
        <li>👑 Adebayo – ₦25,000</li>
        <li>🥈 Chioma – ₦18,000</li>
        <li>🥉 Musa – ₦14,500</li>
      </ol>
    </div>

    <div class="card notice">
      <h3><i class="fa-solid fa-bullhorn"></i> Announcement</h3>
      <p id="announcement">Welcome to PAYEER TECH – Earn smart 💰</p>
    </div>
  </div>
</div>

<!-- TASKS -->
<div id="tasks" class="page">
  <div class="container">
    <div class="card">
      <h3><i class="fa-solid fa-list-check"></i> Available Task</h3>
      <p>Join our official Telegram channel</p>
      <p><b>Reward:</b> ₦1000</p>
      <button onclick="submitTask()">Submit Task</button>
      <p id="taskStatus"></p>
    </div>
  </div>
</div>

<!-- REFERRAL -->
<div id="referral" class="page">
  <div class="container">
    <div class="card">
      <h3><i class="fa-solid fa-user-plus"></i> Referral Link</h3>
      <input id="refLink" readonly />
      <button onclick="copyReferral()">Copy Referral Link</button>
    </div>
  </div>
</div>

<!-- WITHDRAW -->
<div id="withdraw" class="page">
  <div class="container">
    <div class="card">
      <h3><i class="fa-solid fa-building-columns"></i> Withdraw Funds</h3>
      <p>Minimum withdrawal: ₦5000</p>
      <p>Subscription required: ₦2000</p>
      <input placeholder="Bank Name" />
      <input placeholder="Account Number" />
      <input placeholder="Account Name" />
      <button onclick="requestWithdrawal()">Request Withdrawal</button>
      <p id="withdrawStatus"></p>
    </div>
  </div>
</div>

<!-- FLOATING MENU -->
<div class="menu">
  <button onclick="openPage('home')" class="active" id="btn-home"><i class="fa-solid fa-house"></i>Home</button>
  <button onclick="openPage('tasks')" id="btn-tasks"><i class="fa-solid fa-list"></i>Tasks</button>
  <button onclick="openPage('referral')" id="btn-ref"><i class="fa-solid fa-users"></i>Refer</button>
  <button onclick="openPage('withdraw')" id="btn-with"><i class="fa-solid fa-wallet"></i>Withdraw</button>
</div>

<script>
  const userId = '123456789';
  document.getElementById('refLink').value = `https://t.me/PayeerTechBot?start=${userId}`;

  function openPage(page) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(page).classList.add('active');

    document.querySelectorAll('.menu button').forEach(b => b.classList.remove('active'));
    document.getElementById('btn-' + page).classList.add('active');
  }

  function submitTask() {
    document.getElementById('taskStatus').innerText = 'Task submitted. Awaiting admin approval.';
  }

  function copyReferral() {
    navigator.clipboard.writeText(document.getElementById('refLink').value);
    alert('Referral link copied');
  }

  function requestWithdrawal() {
    document.getElementById('withdrawStatus').innerText = 'Withdrawal request sent for admin approval.';
  }
</script>

</body>
</html>
