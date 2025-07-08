<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Silent Witness</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&family=Cairo:wght@400;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --color-bg-light: #ffffff;
      --color-text-light: #1c5980;
      --color-bg-dark: #0e0e0e;
      --color-text-dark: #f1f1f1;
    }

    body {
      margin: 0;
      font-family: 'Poppins', 'Cairo', sans-serif;
      background-color: var(--color-bg-light);
      color: var(--color-text-light);
      transition: background-color 0.3s ease, color 0.3s ease;
    }

    body.dark-mode {
      background-color: var(--color-bg-dark);
      color: var(--color-text-dark);
    }

    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1rem 2rem;
      background-color: #1c5980;
      color: white;
    }

    header select,
    header button {
      margin-left: 1rem;
      padding: 0.4rem 0.6rem;
      font-size: 1rem;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .hero {
      text-align: center;
      padding: 4rem 2rem;
    }

    .animated-text {
      display: inline-block;
      font-size: 2rem;
      font-weight: 700;
      animation: fadeIn 3s infinite;
    }

    @keyframes fadeIn {
      0% { opacity: 0; transform: translateY(-10px); }
      50% { opacity: 1; transform: translateY(0); }
      100% { opacity: 0; transform: translateY(10px); }
    }

    section {
      padding: 2rem;
      max-width: 1000px;
      margin: auto;
    }

    .steps {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1.5rem;
    }

    .step {
      background: #f3f3f3;
      padding: 1rem;
      border-radius: 12px;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
    }

    body.dark-mode .step {
      background: #222;
      color: white;
    }

    .map {
      height: 400px;
      margin-top: 2rem;
    }

    .download-button {
      background: #1c5980;
      color: white;
      padding: 1rem 2rem;
      border-radius: 10px;
      text-decoration: none;
      display: inline-block;
      margin: 2rem 0;
      transition: 0.3s;
    }

    .download-button:hover {
      background: #8fc1a1;
      color: #1c5980;
    }
  </style>
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

  <div class="hero">
    <span class="animated-text" id="hero-message">Vous n'êtes pas seul</span>
  </div>

  <section>
    <h2 id="steps-title">Comment fonctionne Silent Witness ?</h2>
    <div class="steps" id="steps-section">
      <div class="step">🔍 Détection de mots clés dans les échanges IA</div>
      <div class="step">🧠 Analyse croisée avec historique, navigation, ton</div>
      <div class="step">⚠️ Évaluation du niveau de gravité</div>
      <div class="step">📡 Déclenchement d’une alerte automatisée</div>
      <div class="step">📁 Transmission du dossier aux secours ou ONG</div>
    </div>
  </section>

  <section>
    <h2 id="map-title">Carte des suicides dans le monde</h2>
    <div id="map" class="map"></div>
  </section>

  <section>
    <h2 id="whitepaper-title">White Paper</h2>
    <p id="whitepaper-desc">Téléchargez notre livre blanc pour comprendre l'impact de Silent Witness.</p>
    <a href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf" class="download-button" target="_blank" id="whitepaper-button">📘 Télécharger</a>
  </section>

  <section>
    <h2 id="contact-title">Contactez-nous</h2>
    <form id="contact-form">
      <label for="nom">Nom</label>
      <input type="text" id="nom" name="name" required />

      <label for="email">Email</label>
      <input type="email" id="email" name="email" required />

      <label for="message">Message</label>
      <textarea id="message" name="message" required></textarea>

      <button type="submit">Envoyer</button>
    </form>
  </section>

  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script src="https://unpkg.com/leaflet@1.9.3/dist/leaflet.js"></script>
  <script>
    // EmailJS
    emailjs.init('_pR14KMi1syThzlmY');
    document.getElementById('contact-form').addEventListener('submit', function (e) {
      e.preventDefault();
      emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', this)
        .then(() => alert('Message envoyé!'))
        .catch((err) => alert('Erreur: ' + err));
    });

    // Language switching
    const translations = {
      fr: {
        hero: "Vous n'êtes pas seul",
        steps: "Comment fonctionne Silent Witness ?",
        whitepaperTitle: "White Paper",
        whitepaperDesc: "Téléchargez notre livre blanc pour comprendre l'impact de Silent Witness.",
        button: "📘 Télécharger",
        contact: "Contactez-nous",
        map: "Carte des suicides dans le monde"
      },
      en: {
        hero: "You're not alone",
        steps: "How Silent Witness Works",
        whitepaperTitle: "White Paper",
        whitepaperDesc: "Download our white paper to understand Silent Witness impact.",
        button: "📘 Download",
        contact: "Contact Us",
        map: "Global Suicide Map"
      },
      ar: {
        hero: "لست وحدك",
        steps: "كيف يعمل Silent Witness؟",
        whitepaperTitle: "الورقة البيضاء",
        whitepaperDesc: "حمّل الورقة البيضاء الخاصة بنا لفهم تأثير Silent Witness.",
        button: "📘 تحميل",
        contact: "اتصل بنا",
        map: "خريطة الانتحار العالمية"
      }
    };

    document.getElementById('lang-select').addEventListener('change', function () {
      const lang = this.value;
      const t = translations[lang];
      document.getElementById('hero-message').textContent = t.hero;
      document.getElementById('steps-title').textContent = t.steps;
      document.getElementById('whitepaper-title').textContent = t.whitepaperTitle;
      document.getElementById('whitepaper-desc').textContent = t.whitepaperDesc;
      document.getElementById('whitepaper-button').textContent = t.button;
      document.getElementById('contact-title').textContent = t.contact;
      document.getElementById('map-title').textContent = t.map;
    });

    // Dark mode toggle
    document.getElementById('theme-toggle').addEventListener('click', () => {
      document.body.classList.toggle('dark-mode');
    });

    // Map
    const map = L.map('map').setView([20, 0], 2);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '© OpenStreetMap'
    }).addTo(map);

    const suicideRates = [
      { country: "USA", coords: [37.8, -96.9], value: 14.5 },
      { country: "France", coords: [46.6, 2.2], value: 13.0 },
      { country: "India", coords: [20.6, 78.9], value: 12.8 },
      { country: "Japan", coords: [36.2, 138.2], value: 17.5 },
      { country: "Russia", coords: [61, 105], value: 21.1 },
    ];

    suicideRates.forEach(c => {
      L.circle(c.coords, {
        color: 'red',
        radius: c.value * 10000,
        fillOpacity: 0.4
      }).addTo(map).bindPopup(`${c.country}: ${c.value}/100k`);
    });
  </script>
</body>
</html>
