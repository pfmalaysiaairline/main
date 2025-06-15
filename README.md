<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>PF Malaysia Airline</title>
  <link rel="icon" href="https://cdn.discordapp.com/icons/1137786366344525984/a_8a8a2f7a46579b0296f2033cc96243f1.gif" />
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;700&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      font-family: 'Space Grotesk', sans-serif;
      background: radial-gradient(circle at top left, #003366, #000);
      color: white;
      overflow-x: hidden;
      scroll-behavior: smooth;
    }

    /* === NAVBAR === */
    .navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1rem 2rem;
      background-color: rgba(0, 0, 0, 0.8);
      position: sticky;
      top: 0;
      z-index: 999;
      backdrop-filter: blur(10px);
    }

    .navbar-left {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .navbar-left img {
      width: 40px;
      height: 40px;
      border-radius: 50%;
    }

    .navbar-left span {
      font-size: 1.2rem;
      font-weight: bold;
    }

    .navbar-right {
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    .navbar-right a, .navbar-right button {
      background: #5865F2;
      color: white;
      border: none;
      padding: 0.5rem 1rem;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.3s;
      font-size: 1rem;
    }

    .navbar-right button:hover,
    .navbar-right a:hover {
      background: #4752c4;
      transform: scale(1.05);
    }

    header {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 90vh;
      text-align: center;
      padding: 2rem;
      animation: fadeIn 2s ease-in-out;
    }

    header h1 {
      font-size: 3rem;
      animation: floatIn 1.5s ease-out;
    }

    header p {
      margin-top: 1rem;
      font-size: 1.2rem;
      animation: fadeInUp 2s ease-in-out;
    }

    .counter {
      font-size: 2.5rem;
      margin-top: 1rem;
      color: #00ffcc;
      animation: floatIn 1.5s ease-out;
    }

    .user-info {
      margin-top: 1.5rem;
      display: flex;
      align-items: center;
      gap: 1rem;
      animation: fadeInUp 1.5s ease-in-out;
    }

    .user-info img {
      width: 50px;
      height: 50px;
      border-radius: 100%;
    }

    section {
      padding: 4rem 2rem;
      text-align: center;
    }

    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 2rem;
      margin-top: 3rem;
    }

    .card {
      background: #111;
      padding: 2rem;
      border-radius: 1rem;
      transform: translateY(30px);
      opacity: 0;
      animation: fadeUpCard 1s ease forwards;
      transition: 0.4s ease;
    }

    .card:hover {
      transform: scale(1.05) rotate(-1deg);
      box-shadow: 0 0 25px #00bfff88;
    }

    .card:nth-child(2) { animation-delay: 0.3s; }
    .card:nth-child(3) { animation-delay: 0.6s; }
    .card:nth-child(4) { animation-delay: 0.9s; }

    footer {
      background: #111;
      text-align: center;
      padding: 2rem;
      font-size: 0.9rem;
      opacity: 0.8;
    }

    @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
    @keyframes floatIn { from { transform: translateY(-40px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
    @keyframes fadeInUp { from { transform: translateY(30px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
    @keyframes fadeUpCard { to { transform: translateY(0); opacity: 1; } }
    @keyframes pulse { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.05); } }
  </style>
</head>
<body>

<!-- === NAVBAR === -->
<nav class="navbar">
  <div class="navbar-left">
    <img src="" alt="logo">
    <span>PF Malaysia Airline</span>
  </div>
  <div class="navbar-right">
    <div id="user-info" style="display: none;" class="user-info">
      <img id="avatar" src="" alt="Avatar">
      <span id="username"></span>
    </div>
    <a href="https://oauth-gee6k9s5m-pfasc.vercel.app/login" id="login-btn">Login with Discord</a>
  </div>
</nav>

<!-- === HERO SECTION === -->
<header>
  <h1>Welcome to PF Malaysia Airline</h1>
  <p>Flying high in Project Flight's skies 🇲🇾</p>
  <div class="counter" id="memberCount">👥 Loading members...</div>
</header>

<!-- === ABOUT SECTION === -->
<section>
  <h2>About Us</h2>
  <p>We represent Malaysia in Project Flight with passion, professionalism, and fun!</p>
  <div class="cards">
    <div class="card">🛫 Weekly Flights and Events</div>
    <div class="card">🎖️ Ranking System</div>
    <div class="card">🌏 Explore Asia and beyond</div>
    <div class="card">🗣️ Multilingual Friendly Team</div>
  </div>
</section>

<!-- === FOOTER === -->
<footer>
  © 2025 PF Malaysia Airline — All rights reserved.
</footer>

<!-- === JS LOGIC === -->
<script>
  const MEMBER_API = "https://TON_BACKEND_MEMBERS_URL/members"; // Remplace
  const USER_API = "https://oauth-gee6k9s5m-pfasc.vercel.app/user";

  async function updateMemberCount() {
    try {
      const res = await fetch(MEMBER_API);
      const data = await res.json();
      document.getElementById("memberCount").textContent = `👥 ${data.members} Members`;
    } catch (e) {
      document.getElementById("memberCount").textContent = "👥 0 Members";
      console.error("Erreur membres:", e);
    }
  }

  async function fetchUser() {
    try {
      const res = await fetch(USER_API, { credentials: "include" });
      if (!res.ok) return;
      const user = await res.json();
      document.getElementById("user-info").style.display = "flex";
      document.getElementById("username").textContent = user.username;
      document.getElementById("avatar").src = `https://cdn.discordapp.com/avatars/${user.id}/${user.avatar}.png`;
      document.getElementById("login-btn").style.display = "none";
    } catch (e) {
      console.log("Not Connected");
    }
  }

  updateMemberCount();
  fetchUser();
  setInterval(updateMemberCount, 15 * 60 * 1000);
</script>

</body>
</html>
