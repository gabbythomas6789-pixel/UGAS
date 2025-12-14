# UGAS
Develop a secure, cloud-based UGAS website and database to manage members, events, attendance, engagement, and donations. Features include role-based access, online registration, event calendars, QR-code check-ins, media galleries, interactive sky maps, analytics, notifications, and a mobile-friendly, visually engaging interface.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>UGAS Astronomy Platform</title>
<style>
  body { margin:0; font-family:sans-serif; transition: background 0.5s, color 0.5s; }
  header { padding: 20px; background: rgba(0,0,0,0.7); color: white; text-align:center; }
  nav { display:flex; justify-content:center; gap:20px; margin-bottom:20px; flex-wrap:wrap; }
  nav button { padding:10px 20px; cursor:pointer; border:none; border-radius:5px; background:#0077cc; color:white; transition:0.3s; }
  nav button:hover { background:#005fa3; }
  .container { padding:20px; max-width:1000px; margin:auto; }
  .hidden { display:none; }
  .card { padding:15px; margin:10px 0; border:1px solid #ccc; border-radius:8px; background:white; transition:0.3s; }
  .card:hover { transform: translateY(-3px); box-shadow:0 4px 8px rgba(0,0,0,0.2);}
  .dark-mode { background:#0b0b1a; color:white; }
  .dark-mode .card { background:#1c1c3a; border-color:#444; }
  #background { position:fixed; top:0; left:0; width:100%; height:100%; z-index:-1; background-size:cover; background-position:center; transition: background 1s; }
  input, button { font-size:16px; padding:8px; margin:4px 0; width:100%; max-width:400px; }
  h1, h2 { margin:0 0 10px 0; }
  ul { padding-left: 20px; }
</style>
</head>
<body>
<div id="background"></div>
<header>
  <h1>University of Guyana Astronomy Association (UGAS)</h1>
  <button id="toggleMode">Toggle Dark/Light Mode</button>
</header>
<nav>
  <button onclick="showSection('home')">Home</button>
  <button onclick="showSection('register')">Register</button>
  <button onclick="showSection('events')">Events</button>
  <button onclick="showSection('dashboard')">Dashboard</button>
  <button onclick="showSection('gallery')">Gallery</button>
  <button onclick="showSection('skymap')">Sky Map</button>
</nav>

<div class="container">
  <section id="home">
    <h2>Welcome to UGAS!</h2>
    <p>Explore astronomy events, join as a member, and enjoy interactive astronomy content.</p>
  </section>

  <section id="register" class="hidden">
    <h2>Register</h2>
    <form id="regForm">
      <input type="text" placeholder="First Name" required><br>
      <input type="text" placeholder="Last Name" required><br>
      <input type="email" placeholder="Email" required><br>
      <input type="tel" placeholder="Phone"><br>
      <input type="text" placeholder="Region"><br>
      <input type="text" placeholder="Student Status"><br>
      <input type="text" placeholder="USI (if student)"><br>
      <button type="submit">Register</button>
    </form>
    <p id="regMsg"></p>
  </section>

  <section id="events" class="hidden">
    <h2>Upcoming Events</h2>
    <div class="card">🌌 Stargazing Night - Nov 20, 2025</div>
    <div class="card">🪐 Astronomy Lecture - Nov 25, 2025</div>
    <div class="card">🌠 Meteor Shower Viewing - Dec 10, 2025</div>
  </section>

  <section id="dashboard" class="hidden">
    <h2>Your Dashboard</h2>
    <p><strong>Name:</strong> <span id="userName">Guest</span></p>
    <p><strong>Registered Events:</strong></p>
    <ul id="userEvents">
      <li>No events registered yet.</li>
    </ul>
  </section>

  <section id="gallery" class="hidden">
    <h2>Astrophotography Gallery</h2>
    <div class="card">🖼 Milky Way - Photo by Student A</div>
    <div class="card">🖼 Jupiter - Photo by Student B</div>
    <div class="card">🖼 Orion Nebula - Photo by Student C</div>
  </section>

  <section id="skymap" class="hidden">
    <h2>Sky Map / Object of the Week</h2>
    <p>⭐ This Week: Andromeda Galaxy</p>
    <div class="card">[Interactive sky map placeholder]</div>
  </section>
</div>

<script>
const sections = ['home','register','events','dashboard','gallery','skymap'];
function showSection(id){
  sections.forEach(sec => document.getElementById(sec).classList.add('hidden'));
  document.getElementById(id).classList.remove('hidden');
}

// Dark mode toggle
document.getElementById('toggleMode').onclick = ()=> {
  document.body.classList.toggle('dark-mode');
};

// Registration simulation
document.getElementById('regForm').onsubmit = (e)=> {
  e.preventDefault();
  const name = e.target[0].value + " " + e.target[1].value;
  document.getElementById('userName').innerText = name;
  document.getElementById('userEvents').innerHTML = "<li>🌌 Stargazing Night - Nov 20, 2025</li>";
  document.getElementById('regMsg').innerText = "✅ Registration successful! Welcome, " + name;
  showSection('dashboard');
};

// Weekly rotating background
const backgrounds = [
  'https://cdn.pixabay.com/photo/2013/07/18/10/56/milky-way-163096_1280.jpg',
  'https://cdn.pixabay.com/photo/2016/11/29/03/53/space-1867464_1280.jpg',
  'https://cdn.pixabay.com/photo/2014/04/03/10/32/orion-312080_1280.jpg'
];
Date.prototype.getWeek = function() {
  const d = new Date(this.getFullYear(), 0, 1);
  return Math.ceil((((this - d) / 86400000) + d.getDay() + 1)/7);
};
let index = new Date().getWeek() % backgrounds.length;
document.getElementById('background').style.backgroundImage = 'url('+backgrounds[index]+')';
</script>
</body>
</html>
