<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Silent Witness</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&family=Cairo&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
  <style>
    body {
      font-family: 'Poppins', 'Cairo', sans-serif;
      margin: 0;
      background-color: var(--bg);
      color: var(--text);
      transition: background 0.3s, color 0.3s;
    }
    :root {
      --bg: #ffffff;
      --text: #1c5980;
    }
    [data-theme="dark"] {
      --bg: #121212;
      --text: #f0f0f0;
    }
    header {
      padding: 1rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .lang-switcher, .theme-toggle {
      font-size: 1rem;
      margin-left: 1rem;
    }
    .animated-text {
      font-size: 2rem;
      font-weight: bold;
      text-align: center;
      animation: pulseText 2s infinite;
    }
    @keyframes pulseText {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.7; transform: scale(1.05); }
    }
    .carousel {
      display: flex;
      overflow-x: auto;
      scroll-snap-type: x mandatory;
      gap: 1rem;
      padding: 1rem;
    }
    .carousel img {
      width: 100%;
      max-width: 300px;
      border-radius: 12px;
      scroll-snap-align: start;
    }
    .steps {
      max-width: 800px;
      margin: auto;
      padding: 2rem;
    }
    .steps h2, .stats h2, .whitepaper h2 { text-align: center; }
    .step {
      margin-bottom: 1rem;
      padding: 1rem;
      border-left: 4px solid #1c5980;
      background: #f4f9fc;
    }
    .whitepaper, .contact {
      text-align: center;
      padding: 2rem;
    }
    .whitepaper a {
      padding: 1rem 2rem;
      background: #1c5980;
      color: white;
      border-radius: 8px;
      text-decoration: none;
    }
    #map { height: 400px; margin: 2rem auto; max-width: 90%; border-radius: 12px; }
  </style>
</head>
<body>
  <header>
    <h1>Silent Witness</h1>
    <div>
      <select id="language" class="lang-switcher">
        <option value="fr">Français</option>
        <option value="en">English</option>
        <option value="ar">العربية</option>
      </select>
      <button onclick="toggleTheme()" class="theme-toggle">🌓</button>
    </div>
  </header>

  <section class="animated-text">You're not alone</section>

  <section class="carousel">
    <img src="https://source.unsplash.com/featured/?ai,human" alt="IA et humain">
    <img src="https://source.unsplash.com/featured/?technology,help" alt="Technologie et aide">
    <img src="https://source.unsplash.com/featured/?emotion,face" alt="Émotion et visage">
  </section>

  <section class="steps">
    <h2>Fonctionnement de Silent Witness</h2>
    <div class="step">1. Détection des mots-clés dans les discussions avec l’IA et les recherches web</div>
    <div class="step">2. Analyse des signaux vocaux, expressions et fréquence de détresse</div>
    <div class="step">3. Attribution d’un niveau de gravité basé sur l’historique</div>
    <div class="step">4. Dépassement du seuil critique → Alerte automatique</div>
    <div class="step">5. Envoi du dossier chiffré à la police ou ONG partenaire</div>
  </section>

  <section class="stats">
    <h2>Statistiques mondiales sur le suicide</h2>
    <div id="map"></div>
    <p style="text-align:center">Un suicide toutes les 40 secondes dans le monde.</p>
  </section>

  <section class="whitepaper">
    <h2>Livre Blanc</h2>
    <a href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf" target="_blank">📘 Télécharger notre White Paper</a>
  </section>

  <section class="contact">
    <h2>Contactez-nous</h2>
    <form id="contact-form">
      <input type="text" name="nom" placeholder="Votre nom" required><br>
      <input type="email" name="email" placeholder="Votre email" required><br>
      <textarea name="message" placeholder="Votre message" required></textarea><br>
      <button type="submit">Envoyer</button>
    </form>
  </section>

  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
  <script>
    emailjs.init('_pR14KMi1syThzlmY');
    document.getElementById('contact-form').addEventListener('submit', function(e) {
      e.preventDefault();
      emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', this)
        .then(() => alert('Message envoyé !'))
        .catch(() => alert('Erreur lors de l’envoi.'));
    });

    function toggleTheme() {
      document.body.dataset.theme = document.body.dataset.theme === 'dark' ? '' : 'dark';
    }

    const map = L.map('map').setView([20, 0], 2);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; OpenStreetMap contributors'
    }).addTo(map);
    const suicideData = {
      "Asia": 200000,
      "Africa": 100000,
      "Europe": 150000,
      "Americas": 180000
    };
    for (const region in suicideData) {
      L.circle([Math.random()*180 - 90, Math.random()*360 - 180], {
        color: 'red',
        fillColor: '#f03',
        fillOpacity: 0.5,
        radius: suicideData[region] * 10
      }).addTo(map).bindPopup(`${region}: ${suicideData[region].toLocaleString()} suicides/an`);
    }
  </script>
</body>
</html>
