<!DOCTYPE html>
<html lang="fr" dir="ltr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Silent Witness</title>
  <style>
    :root {
      --bg-color: #ffffff;
      --text-color: #1c5980;
    }
    .dark-theme {
      --bg-color: #1c1c1c;
      --text-color: #f0f0f0;
    }
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background-color: var(--bg-color);
      color: var(--text-color);
      transition: background 0.3s, color 0.3s;
    }
    header {
      padding: 1rem;
      background: #204d7a;
      color: white;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .language-select, .theme-toggle {
      margin: 0 10px;
    }
    .animated-text {
      font-size: 2rem;
      font-weight: bold;
      text-align: center;
      margin: 2rem 0;
      animation: pulseText 2s infinite;
    }
    @keyframes pulseText {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.6; transform: scale(1.05); }
    }
    .section {
      padding: 2rem;
      max-width: 1000px;
      margin: auto;
    }
    .download-btn {
      display: inline-block;
      background: #1c5980;
      color: white;
      padding: 0.8rem 1.5rem;
      border-radius: 8px;
      text-decoration: none;
      font-weight: bold;
      transition: 0.3s;
    }
    .download-btn:hover {
      background: #8fc1a1;
      color: #1c5980;
    }
    iframe {
      width: 100%;
      height: 500px;
      border: none;
      margin-top: 2rem;
    }
    form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      margin-top: 2rem;
    }
    input, textarea {
      padding: 0.8rem;
      border-radius: 6px;
      border: 1px solid #ccc;
    }
    button {
      padding: 0.8rem;
      background: #204d7a;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }
    img.header-img {
      width: 100%;
      max-height: 300px;
      object-fit: cover;
      display: block;
      margin-bottom: 2rem;
    }
    [dir="rtl"] {
      direction: rtl;
      text-align: right;
    }
  </style>
  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script src="https://www.paypal.com/sdk/js?client-id=BAAwNQmuQNtmwbB198XpnMFgJqBHvKNcvg138E9ddcIrNxHGCrGT2tvdVOyLaJTqde8dM-9e9ZglZUXS9A&components=hosted-buttons&disable-funding=venmo&currency=USD"></script>
  <script>
    emailjs.init('_pR14KMi1syThzlmY');

    function sendEmail(e) {
      e.preventDefault();
      emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', e.target)
        .then(() => alert('Message envoyé!'))
        .catch(error => alert('Erreur: ' + error));
    }

    const translations = {
      fr: {
        dir: "ltr",
        title: "Vous n'êtes pas seul",
        whitepaper: "📘 Télécharger notre White Paper",
        paragraph: "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.",
        donate: "Faire un don pour soutenir le projet"
      },
      en: {
        dir: "ltr",
        title: "You're not alone",
        whitepaper: "📘 Download our White Paper",
        paragraph: "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable.",
        donate: "Donate to support the project"
      },
      ar: {
        dir: "rtl",
        title: "لست وحدك",
        whitepaper: "📘 تحميل الورقة البيضاء",
        paragraph: "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر.",
        donate: "ساهم لدعم هذا المشروع"
      }
    };

    function updateLanguage(lang) {
      const trans = translations[lang];
      document.documentElement.lang = lang;
      document.documentElement.dir = trans.dir;
      document.querySelector('.animated-text').textContent = trans.title;
      document.getElementById('wp-paragraph').textContent = trans.paragraph;
      document.getElementById('wp-btn').textContent = trans.whitepaper;
      document.getElementById('donate-label').textContent = trans.donate;
    }

    function toggleTheme() {
      document.body.classList.toggle('dark-theme');
    }

    window.onload = () => {
      document.getElementById('contact-form').addEventListener('submit', sendEmail);
      document.getElementById('lang-select').addEventListener('change', (e) => updateLanguage(e.target.value));
      document.getElementById('theme-toggle').addEventListener('click', toggleTheme);
      updateLanguage('fr');
    }
  </script>
</head>
<body>
  <header>
    <h1>Silent Witness</h1>
    <div>
      <select id="lang-select" class="language-select">
        <option value="fr">Français</option>
        <option value="en">English</option>
        <option value="ar">العربية</option>
      </select>
      <button id="theme-toggle" class="theme-toggle">🌓</button>
    </div>
  </header>

  <img class="header-img" src="https://images.unsplash.com/photo-1603394644811-ff8bd13c6e5f?fit=crop&w=1200&q=80" alt="IA et humain en connexion" />

  <div class="animated-text"></div>

  <section class="section">
    <p id="wp-paragraph"></p>
    <a id="wp-btn" href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf" target="_blank" class="download-btn"></a>
  </section>

  <section class="section">
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Carte mondiale des suicides</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background-color: #f5f5f5;
      color: #1c1c1c;
    }
    #map {
      height: 100vh;
      width: 100%;
    }
    .counter {
      position: absolute;
      top: 10px;
      right: 10px;
      background: rgba(0,0,0,0.7);
      color: white;
      padding: 10px 20px;
      border-radius: 8px;
      font-size: 1.2rem;
      z-index: 1000;
    }
    .legend {
      position: absolute;
      bottom: 30px;
      left: 10px;
      background: white;
      padding: 10px;
      border-radius: 5px;
      font-size: 0.9rem;
      box-shadow: 0 2px 6px rgba(0,0,0,0.2);
    }
    .legend div {
      margin-bottom: 5px;
    }
  </style>
</head>
<body>
<div id="map"></div>
<div class="counter" id="suicide-counter">🕯️ 0 suicides depuis l'ouverture</div>
<div class="legend">
  <strong>Légende :</strong><br>
  <div><span style="background:red;width:12px;height:12px;display:inline-block;margin-right:5px;"></span> Taux élevé</div>
  <div><span style="background:orange;width:12px;height:12px;display:inline-block;margin-right:5px;"></span> Taux modéré</div>
  <div><span style="background:green;width:12px;height:12px;display:inline-block;margin-right:5px;"></span> Taux faible</div>
</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script>
  // Base Leaflet
  const map = L.map('map').setView([20, 0], 2);
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; OpenStreetMap contributors'
  }).addTo(map);

  // Taux fictifs par continent (en pour 100k)
  const suicideRates = {
    "Africa": 11.0,
    "Asia": 14.2,
    "Europe": 13.5,
    "North America": 9.2,
    "South America": 6.4,
    "Oceania": 10.1
  };

  const continents = {
    "Africa": [0, 20],
    "Asia": [30, 30],
    "Europe": [55, 15],
    "North America": [40, -100],
    "South America": [-15, -60],
    "Oceania": [-25, 140]
  };

  for (const [name, coord] of Object.entries(continents)) {
    const rate = suicideRates[name];
    const color = rate > 12 ? 'red' : rate > 8 ? 'orange' : 'green';
    L.circle(coord, {
      color,
      fillColor: color,
      fillOpacity: 0.5,
      radius: 1000000
    }).addTo(map).bindPopup(`<b>${name}</b><br>Taux de suicide : ${rate}/100k`);
  }

  // Compteur dynamique
  let counter = 0;
  setInterval(() => {
    counter++;
    document.getElementById('suicide-counter').innerText = `🕯️ ${counter} suicides depuis l'ouverture`;
  }, 40000); // 40 secondes
</script>
</body>
</html>


