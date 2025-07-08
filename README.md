<!DOCTYPE html>
<html lang="fr" dir="ltr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Silent Witness</title>
<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&family=Cairo&display=swap" rel="stylesheet" />
<!-- Leaflet CSS -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.3/dist/leaflet.css" />
<style>
  :root {
    --clr-primary: #1c5980;
    --clr-secondary: #8fc1a1;
    --clr-bg-light: #f8fafb;
    --clr-bg-dark: #1c1c1c;
    --clr-text-light: #1c5980;
    --clr-text-dark: #f0f0f0;
  }
  body {
    margin: 0; padding: 0;
    font-family: 'Poppins', sans-serif;
    background-color: var(--clr-bg-light);
    color: var(--clr-text-light);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    transition: background-color 0.3s, color 0.3s;
  }
  body.dark-theme {
    background-color: var(--clr-bg-dark);
    color: var(--clr-text-dark);
  }
  header {
    background: var(--clr-primary);
    color: white;
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  header h1 {
    font-family: 'Cairo', sans-serif;
    font-weight: 600;
    font-size: 1.8rem;
    margin: 0;
  }
  .controls {
    display: flex;
    gap: 1rem;
    align-items: center;
  }
  select, button.theme-toggle {
    font-size: 1rem;
    padding: 0.3rem 0.6rem;
    border-radius: 5px;
    border: none;
    cursor: pointer;
  }
  button.theme-toggle {
    background: var(--clr-secondary);
    color: var(--clr-primary);
    font-weight: 600;
  }
  button.theme-toggle:hover {
    background: #72a886;
  }
  main {
    flex-grow: 1;
    max-width: 1100px;
    margin: 2rem auto 4rem;
    width: 90%;
  }
  .hero {
    position: relative;
    background: url('https://images.unsplash.com/photo-1524504388940-b1c1722653e1?auto=format&fit=crop&w=1350&q=80') center/cover no-repeat;
    height: 280px;
    border-radius: 12px;
    box-shadow: 0 0 25px rgb(28 89 128 / 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    text-shadow: 0 0 8px rgba(0,0,0,0.8);
  }
  .animated-text {
    font-family: 'Cairo', sans-serif;
    font-size: 2.8rem;
    font-weight: 700;
    animation: fadePulse 3s ease-in-out infinite;
    text-align: center;
    max-width: 90%;
  }
  @keyframes fadePulse {
    0%,100% {opacity:1; transform: scale(1);}
    50% {opacity:0.65; transform: scale(1.07);}
  }

  section {
    margin-top: 3rem;
    padding: 1rem 1.5rem;
    background: var(--clr-bg-light);
    border-radius: 10px;
    box-shadow: 0 0 10px rgb(28 89 128 / 0.15);
    transition: background-color 0.3s;
  }
  body.dark-theme section {
    background: #27353a;
  }
  section h2 {
    font-family: 'Cairo', sans-serif;
    color: var(--clr-primary);
    font-weight: 700;
    margin-bottom: 1rem;
    font-size: 1.6rem;
  }
  section p, section li {
    font-size: 1.1rem;
    line-height: 1.5;
  }
  ul, ol {
    padding-left: 1.4rem;
  }
  /* Form */
  form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  input, textarea {
    font-size: 1rem;
    padding: 0.7rem;
    border-radius: 8px;
    border: 1px solid #ccc;
    font-family: 'Poppins', sans-serif;
  }
  input:focus, textarea:focus {
    border-color: var(--clr-primary);
    outline: none;
  }
  textarea {
    resize: vertical;
    min-height: 100px;
  }
  button.submit-btn {
    background-color: var(--clr-primary);
    color: white;
    font-weight: 700;
    padding: 0.9rem;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 1.1rem;
    transition: background-color 0.3s;
  }
  button.submit-btn:hover {
    background-color: var(--clr-secondary);
    color: var(--clr-primary);
  }
  /* Download button */
  .download-btn {
    display: inline-block;
    margin-top: 0.7rem;
    background: var(--clr-primary);
    color: white;
    padding: 0.8rem 1.6rem;
    border-radius: 10px;
    font-weight: 700;
    text-decoration: none;
    transition: background-color 0.3s;
  }
  .download-btn:hover {
    background: var(--clr-secondary);
    color: var(--clr-primary);
  }
  /* Leaflet Map */
  #map {
    height: 420px;
    border-radius: 12px;
    box-shadow: 0 0 25px rgb(28 89 128 / 0.3);
  }
  /* Paypal Donation */
  .donation-section {
    margin-top: 3rem;
    padding: 1.5rem;
    background: var(--clr-secondary);
    border-radius: 12px;
    color: var(--clr-primary);
    text-align: center;
    box-shadow: 0 0 20px rgb(28 89 128 / 0.25);
  }
  .donation-section h2 {
    color: var(--clr-primary);
    margin-bottom: 1rem;
  }
  .paypal-btn {
    margin-top: 1rem;
    background: #ffc439;
    border: none;
    padding: 12px 30px;
    border-radius: 50px;
    font-weight: 700;
    color: #333;
    cursor: pointer;
    font-size: 1.1rem;
    transition: filter 0.3s;
  }
  .paypal-btn:hover {
    filter: brightness(1.1);
  }
  /* Footer */
  footer {
    text-align: center;
    padding: 1rem;
    background: var(--clr-primary);
    color: white;
    font-family: 'Cairo', sans-serif;
  }
  /* Responsive */
  @media (max-width: 700px) {
    .animated-text {
      font-size: 1.8rem;
      padding: 0 1rem;
    }
    header {
      flex-direction: column;
      gap: 0.7rem;
      align-items: flex-start;
    }
    main {
      width: 95%;
      margin: 1rem auto 3rem;
    }
  }
</style>

<!-- Leaflet JS -->
<script src="https://unpkg.com/leaflet@1.9.3/dist/leaflet.js"></script>
<!-- EmailJS SDK -->
<script src="https://cdn.emailjs.com/dist/email.min.js"></script>
<script>
  // Init EmailJS with your public key
  emailjs.init('_pR14KMi1syThzlmY');

  // Translations for multilingual
  const translations = {
    fr: {
      dir: "ltr",
      title: "Vous n'êtes pas seul",
      whitepaper: "📘 Télécharger notre White Paper",
      paragraph: "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.",
      statsTitle: "Statistiques clés",
      stats: [
        "Près de 800 000 personnes se suicident chaque année (OMS).",
        "1 suicide toutes les 40 secondes dans le monde.",
        "Le suicide est la 2ᵉ cause de mortalité chez les 15-29 ans."
      ],
      detectionTitle: "Étapes de détection IA",
      detectionSteps: [
        "Analyse des mots clés dans les messages, requêtes IA ou recherches web.",
        "Corrélation des données vocales, textuelles ou comportementales.",
        "Évaluation automatique du niveau de détresse.",
        "Classement de l’urgence (vert / orange / rouge).",
        "Déclenchement d'une alerte vers ONG, autorités ou hôpitaux selon le niveau."
      ],
      contactTitle: "Contact",
      contactSubmit: "Envoyer",
      donationTitle: "Soutenez Silent Witness",
      donationText: "Votre don nous aide à concrétiser ce projet et sauver des vies. Merci pour votre générosité.",
      payPalButton: "Faire un don via PayPal",
      whitepaperLink: "https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf"
    },
    en: {
      dir: "ltr",
      title: "You're not alone",
      whitepaper: "📘 Download our White Paper",
      paragraph: "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable.",
      statsTitle: "Key Statistics",
      stats: [
        "Nearly 800,000 people die by suicide every year (WHO).",
        "1 suicide every 40 seconds worldwide.",
        "Suicide is the 2nd leading cause of death among 15-29 year olds."
      ],
      detectionTitle: "AI Detection Steps",
      detectionSteps: [
        "Analyze keywords in messages, AI requests or web searches.",
        "Correlate voice, text or behavioral data.",
        "Automatically assess distress level.",
        "Urgency classification (green / orange / red).",
        "Trigger alert to NGOs, authorities or hospitals accordingly."
      ],
      contactTitle: "Contact",
      contactSubmit: "Send",
      donationTitle: "Support Silent Witness",
      donationText: "Your donation helps us realize this project and save lives. Thank you for your generosity.",
      payPalButton: "Donate via PayPal",
      whitepaperLink: "https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf"
    },
    ar: {
      dir: "rtl",
      title: "لست وحدك",
      whitepaper: "📘 تحميل الورقة البيضاء",
      paragraph: "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر.",
      statsTitle: "الإحصاءات الرئيسية",
      stats: [
        "ينتحر ما يقرب من 800,000 شخص كل عام (منظمة الصحة العالمية).",
        "انتحار واحد كل 40 ثانية في جميع أنحاء العالم.",
        "الانتحار هو السبب الثاني للوفاة بين سن 15-29 عامًا."
      ],
      detectionTitle: "خطوات الكشف بالذكاء الاصطناعي",
      detectionSteps: [
        "تحليل الكلمات المفتاحية في الرسائل أو طلبات الذكاء الاصطناعي أو البحث على الويب.",
        "ربط البيانات الصوتية أو النصية أو السلوكية.",
        "التقييم التلقائي لمستوى الضيق.",
        "تصنيف درجة الطوارئ (أخضر / برتقالي / أحمر).",
        "إطلاق تنبيه إلى المنظمات أو السلطات أو المستشفيات حسب المستوى."
      ],
      contactTitle: "اتصل بنا",
      contactSubmit: "إرسال",
      donationTitle: "ادعم Silent Witness",
      donationText: "يساعدنا تبرعك في تحقيق هذا المشروع وإنقاذ الأرواح. شكرًا لك على سخائك.",
      payPalButton: "تبرع عبر PayPal",
      whitepaperLink: "https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf"
    }
  };

  // Update page content for selected language
  function updateLanguage(lang) {
    const t = translations[lang];
    document.documentElement.lang = lang;
    document.documentElement.dir = t.dir;
    document.body.dir = t.dir;

    document.querySelector('.animated-text').textContent = t.title;
    document.getElementById('wp-paragraph').textContent = t.paragraph;
    const wpBtn = document.getElementById('wp-btn');
    wpBtn.textContent = t.whitepaper;
    wpBtn.href = t.whitepaperLink;

    document.getElementById('stats-title').textContent = t.statsTitle;
    const statsList = document.getElementById('stats-list');
    statsList.innerHTML = '';
    t.stats.forEach(s => {
      const li = document.createElement('li');
      li.textContent = s;
      statsList.appendChild(li);
    });

    document.getElementById('detection-title').textContent = t.detectionTitle;
    const detectionList = document.getElementById('detection-list');
    detectionList.innerHTML = '';
    t.detectionSteps.forEach(step => {
      const li = document.createElement('li');
      li.textContent = step;
      detectionList.appendChild(li);
    });

    document.getElementById('contact-title').textContent = t.contactTitle;
    document.getElementById('submit-btn').textContent = t.contactSubmit;

    document.getElementById('donation-title').textContent = t.donationTitle;
    document.getElementById('donation-text').textContent = t.donationText;
    document.getElementById('paypal-btn').textContent = t.payPalButton;
  }

  // Toggle dark mode
  function toggleTheme() {
    document.body.classList.toggle('dark-theme');
  }

  // Send contact email
  function sendEmail(e) {
    e.preventDefault();
    emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', e.target)
      .then(() => alert('Message envoyé!'))
      .catch(err => alert('Erreur : ' + err.text));
    e.target.reset();
  }

  // Initialize map and add continent + country layers with sample data
  let map;
  let continentLayer;
  let countryLayer;

  // Sample suicide rates per 100k (fake data for demo)
  const continentData = {
    "Africa": { lat: 1.6508, lng: 17.6791, rate: 7.1 },
    "Asia": { lat: 34.0479, lng: 100.6197, rate: 9.5 },
    "Europe": { lat: 54.5260, lng: 15.2551, rate: 14.8 },
    "North America": { lat: 54.5260, lng: -105.2551, rate: 13.7 },
    "Oceania": { lat: -22.7359, lng: 140.0188, rate: 12.5 },
    "South America": { lat: -8.7832, lng: -55.4915, rate: 8.2 }
  };

  const countryData = {
    "France": { lat: 46.2276, lng: 2.2137, rate: 15.2 },
    "USA": { lat: 37.0902, lng: -95.7129, rate: 13.9 },
    "Brazil": { lat: -14.2350, lng: -51.9253, rate: 7.5 },
    "Japan": { lat: 36.2048, lng: 138.2529, rate: 14.0 },
    "South Africa": { lat: -30.5595, lng: 22.9375, rate: 11.6 },
    "Australia": { lat: -25.2744, lng: 133.7751, rate: 12.3 }
  };

  // Color scale for rates
  function getColor(rate) {
    return rate > 14 ? '#d73027' :
           rate > 12 ? '#fc8d59' :
           rate > 9 ? '#fee08b' :
           rate > 7 ? '#d9ef8b' :
                      '#91cf60';
  }

  function onEachFeature(feature, layer) {
    if (feature.properties && feature.properties.name) {
      layer.bindPopup(`<b>${feature.properties.name}</b><br>Suicide rate: ${feature.properties.rate} per 100k`);
    }
  }

  function addContinentMarkers() {
    Object.entries(continentData).forEach(([continent, info]) => {
      const circle = L.circle([info.lat, info.lng], {
        color: getColor(info.rate),
        fillColor: getColor(info.rate),
        fillOpacity: 0.5,
        radius: info.rate * 30000
      }).addTo(map);
      circle.bindPopup(`<b>${continent}</b><br>Taux moyen de suicide: ${info.rate} / 100k habitants`);
    });
  }

  function addCountryMarkers() {
    Object.entries(countryData).forEach(([country, info]) => {
      const circle = L.circleMarker([info.lat, info.lng], {
        color: getColor(info.rate),
        fillColor: getColor(info.rate),
        fillOpacity: 0.7,
        radius: 12
      }).addTo(map);
      circle.bindPopup(`<b>${country}</b><br>Taux de suicide: ${info.rate} / 100k habitants`);
    });
  }

  window.onload = () => {
    // Initialize EmailJS form handler
    document.getElementById('contact-form').addEventListener('submit', sendEmail);
    // Language selector
    const langSelect = document.getElementById('lang-select');
    langSelect.addEventListener('change', e => updateLanguage(e.target.value));
    // Theme toggle button
    document.getElementById('theme-toggle').addEventListener('click', toggleTheme);

    updateLanguage('fr');

    // Initialize Leaflet map
    map = L.map('map').setView([20, 0], 2);

    // Add OpenStreetMap tile layer
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      maxZoom: 6,
      attribution: '&copy; OpenStreetMap contributors'
    }).addTo(map);

    addContinentMarkers();

    // Show country markers on zoom >=4, hide below
    map.on('zoomend', () => {
      if (map.getZoom() >= 4) {
        addCountryMarkers();
      } else {
        // Remove all country markers - workaround: clear map and redraw continents
        map.eachLayer(layer => {
          if (layer instanceof L.CircleMarker) {
            map.removeLayer(layer);
          }
        });
        addContinentMarkers();
      }
    });
  };
</script>
</head>
<body>
<header>
  <h1>Silent Witness</h1>
  <div class="controls">
    <select id="lang-select" aria-label="Choisir la langue">
      <option value="fr" selected>Français</option>
      <option value="en">English</option>
      <option value="ar">العربية</option>
    </select>
    <button id="theme-toggle" class="theme-toggle" aria-label="Basculer thème clair/sombre">🌓</button>
  </div>
</header>

<main>
  <section class="hero">
    <div class="animated-text" aria-live="polite" aria-atomic="true"></div>
  </section>

  <section aria-label="Présentation du projet">
    <p id="wp-paragraph"></p>
    <a id="wp-btn" class="download-btn" target="_blank" rel="noopener noreferrer" aria-label="Télécharger le white paper"></a>
  </section>

  <section aria-label="Carte mondiale des taux de suicide">
    <h2 id="map-title">Carte mondiale des suicides</h2>
    <div id="map" role="region" aria-label="Carte interactive des taux de suicide par continent et pays"></div>
  </section>

  <section aria-label="Statistiques sur le suicide">
    <h2 id="stats-title"></h2>
    <ul id="stats-list" role="list"></ul>
  </section>

  <section aria-label="Étapes de détection de l'IA">
    <h2 id="detection-title"></h2>
    <ol id="detection-list" role="list"></ol>
  </section>

  <section aria-label="Formulaire de contact">
    <h2 id="contact-title"></h2>
    <form id="contact-form" aria-label="Formulaire de contact">
      <input type="text" name="nom" placeholder="Votre nom" required aria-required="true" />
      <input type="email" name="email" placeholder="Votre email" required aria-required="true" />
      <textarea name="message" placeholder="Votre message" required aria-required="true"></textarea>
      <button type="submit" id="submit-btn" class="submit-btn"></button>
    </form>
  </section>

  <section class="donation-section" aria-label="Section de donation pour soutenir le projet">
    <h2 id="donation-title"></h2>
    <p id="donation-text"></p>
    <form action="https://www.paypal.com/donate" method="post" target="_blank" style="margin-top:1rem;">
      <!-- Remplacez le 'hosted_button_id' par celui généré dans votre compte PayPal -->
      <input type="hidden" name="hosted_button_id" value="UTEPDMT9UCV2S" />
      <button type="submit" class="paypal-btn" aria-label="Faire un don via PayPal"></button>
    </form>
  </section>
</main>

<footer>
  &copy; 2025 Silent Witness – Tous droits réservés
</footer>
</body>
</html>

