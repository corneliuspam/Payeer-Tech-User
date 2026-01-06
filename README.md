<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PAYEER TECH</title>

  <!-- Icons -->
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">

  <style>
    body{
      margin:0;
      background:#000;
      color:#fff;
      font-family:Arial,Helvetica,sans-serif;
    }
    .app{padding-bottom:90px;}
    .header{
      background:#111;
      padding:15px;
      text-align:center;
      font-size:20px;
      font-weight:bold;
      color:#e53935;
    }
    .card{
      background:#111;
      margin:15px;
      padding:15px;
      border-radius:14px;
      box-shadow:0 0 10px rgba(0,0,0,.6);
    }
    .balance{
      background:linear-gradient(135deg,#e53935,#43a047);
      padding:20px;
      border-radius:16px;
      text-align:center;
    }
    .balance h1{margin:5px 0;font-size:30px;}
    .row{display:flex;justify-content:space-between;align-items:center;}
    .btn{
      background:#e53935;
      border:none;
      padding:12px;
      width:100%;
      border-radius:10px;
      color:#fff;
      margin-top:10px;
      font-size:15px;
    }
    .task{
      border-bottom:1px solid #333;
      padding:10px 0;
    }
    .task:last-child{border:none;}
    .bottom-nav{
      position:fixed;
      bottom:0;
      width:100%;
      background:#111;
      display:flex;
      justify-content:space-around;
      padding:10px 0;
      box-shadow:0 -2px 10px rgba(0,0,0,.7);
    }
    .nav-btn{
      color:#aaa;
      text-align:center;
      font-size:12px;
    }
    .nav-btn i{font-size:20px;display:block;margin-bottom:3px;}
    .active{color:#e53935;}
    .page{display:none;}
    .page.active{display:block;}
    .profile{text-align:center;}
    .profile img{
      width:90px;
      height:90px;
      border-radius:50%;
      margin-bottom:10px;
    }
  </style>
</head>
<body>

<div class="header">PAYEER TECH</div>

<div class="app">

  <!-- HOME / WALLET -->
  <div id="home" class="page active">
    <div class="card balance">
      <div>Available Balance</div>
      <h1>₦ <span id="balance">0</span></h1>
      <small>Minimum withdrawal ₦5000</small>
    </div>

    <div class="card">
      <h3>Admin Message</h3>
      <p id="announcement">Welcome to PAYEER TECH</p>
    </div>

    <div class="card">
      <h3>Leaderboard</h3>
      <p>🔥 Top Earners Today</p>
      <ol>
        <li>User123 – ₦25,000</li>
        <li>User456 – ₦18,000</li>
        <li>User789 – ₦12,000</li>
      </ol>
    </div>
  </div>

  <!-- TASKS -->
  <div id="tasks" class="page">
    <div class="card">
      <h3>Available Tasks</h3>
      <div class="task">
        <b>Join Telegram Channel</b>
        <p>Reward: ₦1000</p>
        <button class="btn">Submit Task</button>
      </div>
      <div class="task">
        <b>Follow Instagram Page</b>
        <p>Reward: ₦1000</p>
        <button class="btn">Submit Task</button>
      </div>
    </div>
  </div>

  <!-- REFERRAL -->
  <div id="referral" class="page">
    <div class="card">
      <h3>Your Referral Link</h3>
      <input value="https://t.me/payeertech_bot?start=123456" readonly style="width:100%;padding:10px;border-radius:8px;border:none">
      <button class="btn">Copy Link</button>
      <p>Earn when your referrals complete tasks.</p>
    </div>
  </div>

  <!-- WITHDRAW -->
  <div id="withdraw" class="page">
    <div class="card">
      <h3>Withdraw Earnings</h3>
      <p>Subscription Fee: ₦2000 (required)</p>
      <input placeholder="Bank Name">
      <input placeholder="Account Number">
      <input placeholder="Account Name">
      <button class="btn">Request Withdrawal</button>
    </div>
  </div>

  <!-- PROFILE -->
  <div id="profile" class="page">
    <div class="card profile">
      <img id="avatar" src="https://via.placeholder.com/90">
      <h3 id="username">Telegram User</h3>
      <p>ID: <span id="userid">---</span></p>
      <p>Total Earnings: ₦ <span id="totalearn">0</span></p>
    </div>
  </div>

</div>

<!-- BOTTOM NAV -->
<div class="bottom-nav">
  <div class="nav-btn active" onclick="show('home')"><i class="fa fa-wallet"></i>Home</div>
  <div class="nav-btn" onclick="show('tasks')"><i class="fa fa-list"></i>Tasks</div>
  <div class="nav-btn" onclick="show('referral')"><i class="fa fa-users"></i>Referrals</div>
  <div class="nav-btn" onclick="show('withdraw')"><i class="fa fa-bank"></i>Withdraw</div>
  <div class="nav-btn" onclick="show('profile')"><i class="fa fa-user"></i>Profile</div>
</div>

<script>
  function show(id){
    document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
    event.currentTarget.classList.add('active');
  }

  // Telegram auto load
  if(window.Telegram && Telegram.WebApp){
    const user = Telegram.WebApp.initDataUnsafe.user;
    if(user){
      document.getElementById('username').innerText = user.first_name;
      document.getElementById('userid').innerText = user.id;
      if(user.photo_url) document.getElementById('avatar').src = user.photo_url;
    }
  }
</script>

</body>
</html>
