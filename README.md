<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Silent Witness</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #1c5980;
      --accent: #8fc1a1;
      --bg-light: #ffffff;
      --bg-dark: #1c1c1c;
      --text-light: #1c5980;
      --text-dark: #f0f0f0;
    }
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background-color: var(--bg-light);
      color: var(--text-light);
      transition: 0.3s;
    }
    body.dark-theme {
      background-color: var(--bg-dark);
      color: var(--text-dark);
    }
    header {
      background-color: var(--primary);
      color: white;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    header select, header button {
      margin-left: 1rem;
    }
    .animated-text {
      font-size: 2rem;
      font-weight: 600;
      text-align: center;
      margin: 2rem;
      animation: pulseText 2s infinite;
    }
    @keyframes pulseText {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.7; transform: scale(1.05); }
    }
    .section {
      padding: 2rem;
      max-width: 1000px;
      margin: auto;
    }
    .download-btn, .donate-btn {
      display: inline-block;
      background: var(--primary);
      color: white;
      padding: 0.8rem 1.5rem;
      border-radius: 8px;
      text-decoration: none;
      font-weight: bold;
      transition: 0.3s;
    }
    .download-btn:hover, .donate-btn:hover {
      background: var(--accent);
      color: var(--primary);
    }
    #map {
      height: 500px;
      width: 100%;
      margin-top: 1rem;
      border-radius: 12px;
      box-shadow: 0 0 8px rgba(0,0,0,0.1);
    }
    iframe, img {
      max-width: 100%;
      border-radius: 10px;
    }
    form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
    input, textarea {
      padding: 0.8rem;
      border-radius: 6px;
      border: 1px solid #ccc;
    }
    button {
      padding: 0.8rem;
      background: var(--primary);
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }
    footer {
      text-align: center;
      padding: 1rem;
      background-color: #f0f0f0;
      margin-top: 3rem;
    }
  </style>
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
</head>
<body>
  <header>
    <h1>Silent Witness</h1>
    <div>
      <select id="lang-select">
        <option value="fr">Français</option>
        <option value="en">English</option>
        <option value="ar">العربية</option>
      </select>
      <button id="theme-toggle">🌓</button>
    </div>
  </header>

  <div class="animated-text" id="main-title">Vous n'êtes pas seul</div>

  <section class="section">
    <img src="https://images.unsplash.com/photo-1604779116490-fbdfc02d7ebd" alt="IA et humain" />
    <p id="wp-paragraph">Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.</p>
    <a id="wp-btn" href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf" target="_blank" class="download-btn">📘 Télécharger le White Paper</a>
  </section>

  <section class="section">
    <h2>Carte mondiale des suicides</h2>
    <div id="map"></div>
  </section>

  <section class="section">
    <h2>Statistiques clés</h2>
    <ul>
      <li>Près de 800 000 personnes se suicident chaque année (OMS)</li>
      <li>1 suicide toutes les 40 secondes dans le monde</li>
      <li>Le suicide est la 2e cause de mortalité chez les 15-29 ans</li>
    </ul>
  </section>

  <section class="section">
    <h2>Étapes de détection IA</h2>
    <ol>
      <li>Analyse des mots clés dans les messages ou requêtes</li>
      <li>Corrélation vocale et comportementale</li>
      <li>Évaluation du niveau de détresse</li>
      <li>Classement de l'urgence (vert/orange/rouge)</li>
      <li>Déclenchement d'alerte vers les services compétents</li>
    </ol>
  </section>

  <section class="section">
    <h2>Faire un don</h2>
    <p>Votre soutien nous aide à concrétiser Silent Witness et sauver des vies. Chaque contribution compte ❤️</p>
    <div id="paypal-container-UTEPDMT9UCV2S"></div>
  </section>

  <section class="section">
    <h2>Contact</h2>
    <form id="contact-form">
      <input type="text" name="nom" placeholder="Votre nom" required>
      <input type="email" name="email" placeholder="Votre email" required>
      <textarea name="message" rows="4" placeholder="Votre message" required></textarea>
      <button type="submit">Envoyer</button>
    </form>
  </section>

  <footer>
    <p>&copy; 2025 Silent Witness Team | <a href="https://github.com/silentwitnessteam" target="_blank">GitHub</a></p>
  </footer>

  <script src="https://www.paypal.com/sdk/js?client-id=BAAwNQmuQNtmwbB198XpnMFgJqBHvKNcvg138E9ddcIrNxHGCrGT2tvdVOyLaJTqde8dM-9e9ZglZUXS9A&components=hosted-buttons&disable-funding=venmo&currency=USD"></script>
  <script>
    emailjs.init('_pR14KMi1syThzlmY');
    document.getElementById('contact-form').addEventListener('submit', function(e) {
      e.preventDefault();
      emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', this)
        .then(() => alert('Message envoyé!'))
        .catch(error => alert('Erreur: ' + error));
    });

    paypal.HostedButtons({ hostedButtonId: "UTEPDMT9UCV2S" }).render("#paypal-container-UTEPDMT9UCV2S");

    const translations = {
      fr: {
        title: "Vous n'êtes pas seul",
        whitepaper: "📘 Télécharger le White Paper",
        paragraph: "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables."
      },
      en: {
        title: "You're not alone",
        whitepaper: "📘 Download the White Paper",
        paragraph: "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable."
      },
      ar: {
        title: "لست وحدك",
        whitepaper: "📘 تحميل الورقة البيضاء",
        paragraph: "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر."
      }
    };
    function updateLanguage(lang) {
      document.getElementById('main-title').textContent = translations[lang].title;
      document.getElementById('wp-paragraph').textContent = translations[lang].paragraph;
      document.getElementById('wp-btn').textContent = translations[lang].whitepaper;
      document.body.dir = (lang === 'ar') ? 'rtl' : 'ltr';
    }
    document.getElementById('lang-select').addEventListener('change', e => updateLanguage(e.target.value));
    document.getElementById('theme-toggle').addEventListener('click', () => document.body.classList.toggle('dark-theme'));
    updateLanguage('fr');

    const map = L.map('map').setView([20, 0], 2);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; OpenStreetMap contributors'
    }).addTo(map);
    const data = {
      'Afrique': { coords: [0, 20], value: 10 },
      'Europe': { coords: [54, 15], value: 14 },
      'Asie': { coords: [34, 100], value: 13 },
      'Amérique': { coords: [10, -70], value: 11 },
      'Océanie': { coords: [-20, 130], value: 9 }
    };
    Object.entries(data).forEach(([continent, info]) => {
      L.circle(info.coords, {
        color: 'red', fillColor: '#f03', fillOpacity: 0.5, radius: info.value * 30000
      }).addTo(map).bindPopup(`<b>${continent}</b><br>${info.value} suicides/100k habitants`);
    });
  </script>
</body>
</html>
