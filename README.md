<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Silent Witness</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cairo&family=Poppins:wght@400;600&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" integrity="sha256-sA+e2atCfQ+DfCfjJGLbUoHplT1jz4j8v+QytbAdG20=" crossorigin=""/>
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background-color: var(--bg-color, #ffffff);
      color: var(--text-color, #1c5980);
      transition: background 0.3s, color 0.3s;
    }
    .dark-theme {
      --bg-color: #1c1c1c;
      --text-color: #f0f0f0;
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
      max-width: 900px;
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
    #map {
      height: 500px;
      width: 100%;
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
  </style>
  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js" integrity="sha256-o9N1jRVvxb2F0tvyyxFqH4Md4QbktbDJQ+3j7b3ZE3g=" crossorigin=""></script>
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

  <div class="animated-text" id="animated-text"></div>

  <section class="section">
    <p id="wp-paragraph"></p>
    <a id="wp-btn" href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf" target="_blank" class="download-btn"></a>
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
      <li>Analyse des mots clés dans les messages, requêtes IA ou recherches web</li>
      <li>Corrélation des données vocales, textuelles ou comportementales</li>
      <li>Évaluation automatique du niveau de détresse</li>
      <li>Classement de l’urgence (vert / orange / rouge)</li>
      <li>Déclenchement d'une alerte vers ONG, autorités ou hôpitaux selon le niveau</li>
    </ol>
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

  <section class="section">
    <h2>Soutenez Silent Witness</h2>
    <p>Contribuez à concrétiser ce projet d’IA éthique en faisant un don. Chaque aide compte pour sauver des vies.</p>
    <form action="https://www.paypal.com/donate" method="post" target="_blank">
      <input type="hidden" name="hosted_button_id" value="UTEPDMT9UCV2S" />
      <button type="submit" class="download-btn">Faire un don via PayPal</button>
    </form>
  </section>

  <footer class="section">
    © 2025 Silent Witness. Tous droits réservés.
  </footer>

<script>
  emailjs.init('_pR14KMi1syThzlmY');

  function sendEmail(e) {
    e.preventDefault();
    emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', e.target)
      .then(() => alert('Message envoyé!'))
      .catch(error => alert('Erreur: ' + error));
    e.target.reset();
  }

  const translations = {
    fr: {
      title: "Vous n'êtes pas seul",
      whitepaper: "📘 Télécharger notre White Paper",
      paragraph: "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables."
    },
    en: {
      title: "You're not alone",
      whitepaper: "📘 Download our White Paper",
      paragraph: "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable."
    },
    ar: {
      title: "لست وحدك",
      whitepaper: "📘 تحميل الورقة البيضاء",
      paragraph: "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر."
    }
  };

  function updateLanguage(lang) {
    document.getElementById('animated-text').textContent = translations[lang].title;
    document.getElementById('wp-paragraph').textContent = translations[lang].paragraph;
    document.getElementById('wp-btn').textContent = translations[lang].whitepaper;
    document.body.setAttribute('dir', lang === 'ar' ? 'rtl' : 'ltr');
  }

  function toggleTheme() {
    document.body.classList.toggle('dark-theme');
  }

  window.onload = () => {
    document.getElementById('contact-form').addEventListener('submit', sendEmail);
    document.getElementById('lang-select').addEventListener('change', (e) => updateLanguage(e.target.value));
    document.getElementById('theme-toggle').addEventListener('click', toggleTheme);
    updateLanguage('fr');

    const map = L.map('map').setView([20, 0], 2);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      maxZoom: 10,
      attribution: '© OpenStreetMap'
    }).addTo(map);

    const suicideData = [
      { region: "Afrique", lat: 1.5, lon: 17.5, rate: 6.9 },
      { region: "Europe", lat: 54, lon: 15, rate: 14.1 },
      { region: "Asie", lat: 34, lon: 100, rate: 12.0 },
      { region: "Amérique du Nord", lat: 45, lon: -100, rate: 13.7 },
      { region: "Amérique du Sud", lat: -15, lon: -60, rate: 6.2 },
      { region: "Océanie", lat: -25, lon: 140, rate: 10.8 }
    ];

    suicideData.forEach((entry) => {
      L.circle([entry.lat, entry.lon], {
        color: '#ff5555',
        fillColor: '#ff8888',
        fillOpacity: 0.6,
        radius: entry.rate * 20000
      }).addTo(map).bindPopup(
        `<strong>${entry.region}</strong><br>Taux de suicide moyen : ${entry.rate} pour 100 000`
      );
    });
  };
</script>

</body>
</html>
