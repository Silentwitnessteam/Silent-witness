<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Silent Witness - Prévention & Soutien</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet" />
<!-- Leaflet CSS -->
<link
  rel="stylesheet"
  href="https://unpkg.com/leaflet@1.9.3/dist/leaflet.css"
  integrity="sha256-sA+4a6TCr1FzffKn1xFKfIQ87IjYwvA8r+ZvH5f5smM="
  crossorigin=""
/>

<style>
  :root {
    --color-primary: #1c5980;
    --color-secondary: #8fc1a1;
    --color-bg-light: #f9fafb;
    --color-bg-dark: #121212;
    --color-text-light: #222;
    --color-text-dark: #e0e0e0;
    --transition-speed: 0.3s;
    --border-radius: 12px;
    --font-family: 'Poppins', sans-serif;
  }
  body {
    margin: 0; padding: 0;
    font-family: var(--font-family);
    background: var(--color-bg-light);
    color: var(--color-text-light);
    min-height: 100vh;
    transition: background-color var(--transition-speed), color var(--transition-speed);
  }
  body.dark-theme {
    background: var(--color-bg-dark);
    color: var(--color-text-dark);
  }
  header {
    background: var(--color-primary);
    color: white;
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    user-select: none;
  }
  header h1 {
    margin: 0;
    font-weight: 900;
    font-size: 1.9rem;
    cursor: default;
  }
  #lang-select {
    background: white;
    border-radius: var(--border-radius);
    border: none;
    padding: 0.3rem 0.8rem;
    font-size: 1rem;
    color: var(--color-primary);
    cursor: pointer;
    box-shadow: 0 4px 12px rgba(28, 89, 128, 0.2);
    transition: background-color 0.3s;
  }
  #lang-select:hover, #lang-select:focus {
    background-color: var(--color-secondary);
    color: white;
    outline: none;
  }
  #theme-toggle {
    background: transparent;
    border: none;
    font-size: 1.6rem;
    color: white;
    cursor: pointer;
    margin-left: 1rem;
    transition: color 0.3s;
  }
  #theme-toggle:hover {
    color: var(--color-secondary);
  }

  main {
    max-width: 960px;
    margin: 2rem auto 4rem;
    padding: 0 1rem;
  }
  section {
    margin-bottom: 3rem;
  }
  h2 {
    font-weight: 900;
    font-size: 2rem;
    margin-bottom: 1rem;
    user-select: none;
    color: var(--color-primary);
    text-align: center;
  }

  /* Statistiques */
  #stats-list {
    max-width: 700px;
    margin: 0 auto;
    font-size: 1.15rem;
    line-height: 1.6;
    list-style: inside disc;
    color: inherit;
  }

  /* Carte */
  #map {
    height: 500px;
    max-width: 960px;
    margin: 0 auto;
    border-radius: var(--border-radius);
    box-shadow: 0 8px 20px rgba(28, 89, 128, 0.3);
  }

  /* Formulaire */
  form#contact-form {
    max-width: 480px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  label {
    font-weight: 600;
    color: var(--color-primary);
  }
  input, textarea {
    font-family: var(--font-family);
    font-size: 1rem;
    padding: 0.9rem 1.2rem;
    border-radius: var(--border-radius);
    border: 2px solid #ccc;
    resize: vertical;
    color: var(--color-text-light);
  }
  body.dark-theme input, body.dark-theme textarea {
    background: #222;
    border-color: #555;
    color: var(--color-text-dark);
  }
  input:focus, textarea:focus {
    outline: none;
    border-color: var(--color-primary);
    box-shadow: 0 0 12px rgba(28,89,128,0.4);
  }
  button[type="submit"] {
    background: var(--color-primary);
    color: white;
    font-weight: 700;
    padding: 1rem;
    border: none;
    border-radius: var(--border-radius);
    cursor: pointer;
    font-size: 1.2rem;
    transition: background-color 0.3s ease;
  }
  button[type="submit"]:hover {
    background: var(--color-secondary);
    color: var(--color-primary);
  }
  .error-msg {
    color: #c0392b;
    font-size: 0.85rem;
    font-weight: 600;
    display: none;
  }
  .error-msg.active {
    display: block;
  }

  /* Soutenir bouton */
  #support-btn {
    display: block;
    max-width: 220px;
    margin: 1rem auto 3rem;
    background: var(--color-primary);
    color: white;
    border: none;
    padding: 1rem 1.5rem;
    font-weight: 700;
    font-size: 1.15rem;
    border-radius: var(--border-radius);
    cursor: pointer;
    box-shadow: 0 6px 18px rgba(28, 89, 128, 0.4);
    transition: background-color 0.3s ease;
    user-select: none;
  }
  #support-btn:hover {
    background: var(--color-secondary);
    color: var(--color-primary);
  }

  /* Responsive */
  @media (max-width: 600px) {
    #map {
      height: 350px;
    }
    form#contact-form {
      max-width: 100%;
    }
  }

  /* RTL support for Arabic */
  html[lang="ar"] {
    direction: rtl;
    text-align: right;
  }
  html[lang="ar"] label {
    text-align: right;
  }
  html[lang="ar"] input, html[lang="ar"] textarea {
    direction: rtl;
    text-align: right;
  }
</style>
</head>
<body>

<header>
  <h1 data-lang-fr="Silent Witness" data-lang-en="Silent Witness" data-lang-ar="الشاهد الصامت">Silent Witness</h1>
  <div>
    <select id="lang-select" aria-label="Choisir la langue">
      <option value="fr" selected>Français</option>
      <option value="en">English</option>
      <option value="ar">العربية</option>
    </select>
    <button id="theme-toggle" aria-label="Toggle Dark Mode">🌙</button>
  </div>
</header>

<main>
  <section id="stats-section">
    <h2 data-lang-fr="Statistiques Clés" data-lang-en="Key Statistics" data-lang-ar="إحصائيات رئيسية">Statistiques Clés</h2>
    <ul id="stats-list">
      <li data-lang-fr="Environ 700 000 décès par suicide chaque année dans le monde." data-lang-en="Approximately 700,000 deaths by suicide annually worldwide." data-lang-ar="حوالي 700,000 حالة وفاة بسبب الانتحار سنويًا في العالم."></li>
      <li data-lang-fr="Le suicide est la deuxième cause de mortalité chez les jeunes de 15 à 29 ans." data-lang-en="Suicide is the second leading cause of death among 15-29 year olds." data-lang-ar="الانتحار هو السبب الثاني للوفاة بين الشباب من 15 إلى 29 عامًا."></li>
      <li data-lang-fr="30% des femmes dans le monde subissent des violences conjugales." data-lang-en="30% of women worldwide experience intimate partner violence." data-lang-ar="30٪ من النساء في العالم يتعرضن للعنف من الشريك الحميم."></li>
      <li data-lang-fr="Le taux de suicide au Maroc est d'environ 3.9 pour 100 000 habitants." data-lang-en="Morocco's suicide rate is approximately 3.9 per 100,000 people." data-lang-ar="معدل الانتحار في المغرب حوالي 3.9 لكل 100,000 نسمة."></li>
      <li data-lang-fr="Les taux de suicide varient selon les continents, avec les plus élevés en Europe et en Asie." data-lang-en="Suicide rates vary by continent, highest in Europe and Asia." data-lang-ar="تختلف معدلات الانتحار حسب القارات، الأعلى في أوروبا وآسيا."></li>
    </ul>
  </section>

  <section id="map-section">
    <h2 data-lang-fr="Carte mondiale du suicide" data-lang-en="World Suicide Map" data-lang-ar="خريطة الانتحار العالمية">Carte mondiale du suicide</h2>
    <div id="map" role="region" aria-label="Carte montrant les taux de suicide par pays"></div>
  </section>

  <button id="support-btn" data-lang-fr="Soutenir le projet" data-lang-en="Support the Project" data-lang-ar="دعم المشروع" type="button"></button>

  <section id="contact-section">
    <h2 data-lang-fr="Contactez-nous" data-lang-en="Contact Us" data-lang-ar="اتصل بنا">Contactez-nous</h2>
    <form id="contact-form" novalidate>
      <label for="name" data-lang-fr="Nom" data-lang-en="Name" data-lang-ar="الاسم">Nom</label>
      <input
        type="text"
        id="name"
        name="name"
        placeholder="Votre nom"
        required
        data-placeholder-fr="Votre nom"
        data-placeholder-en="Your name"
        data-placeholder-ar="اسمك"
        aria-describedby="name-error"
      />
      <div id="name-error" class="error-msg" aria-live="polite" role="alert">Veuillez entrer votre nom.</div>

      <label for="email" data-lang-fr="Email" data-lang-en="Email" data-lang-ar="البريد الإلكتروني">Email</label>
      <input
        type="email"
        id="email"
        name="email"
        placeholder="Votre email"
        required
        data-placeholder-fr="Votre email"
        data-placeholder-en="Your email"
        data-placeholder-ar="بريدك الإلكتروني"
        aria-describedby="email-error"
      />
      <div id="email-error" class="error-msg" aria-live="polite" role="alert">Veuillez entrer un email valide.</div>

      <label for="message" data-lang-fr="Message" data-lang-en="Message" data-lang-ar="رسالتك">Message</label>
      <textarea
        id="message"
        name="message"
        rows="5"
        placeholder="Votre message"
        required
        data-placeholder-fr="Votre message"
        data-placeholder-en="Your message"
        data-placeholder-ar="رسالتك"
        aria-describedby="message-error"
      ></textarea>
      <div id="message-error" class="error-msg" aria-live="polite" role="alert">Le message ne peut pas être vide.</div>

      <button type="submit" data-lang-fr="Envoyer" data-lang-en="Send" data-lang-ar="إرسال">Envoyer</button>
    </form>
  </section>
</main>

<!-- Leaflet JS -->
<script
  src="https://unpkg.com/leaflet@1.9.3/dist/leaflet.js"
  integrity="sha256-nnp2HAfHnsjTv/yf3tqMjcxl9B4QSpz4hQZjPSZV2kM="
  crossorigin=""
></script>

<script>
  // === Gestion langue (FR/EN/AR) ===
  const langSelect = document.getElementById('lang-select');
  const allLangElements = document.querySelectorAll('[data-lang-fr]');

  function updateLanguage(lang) {
    document.documentElement.lang = lang;
    if (lang === 'ar') {
      document.documentElement.dir = 'rtl';
    } else {
      document.documentElement.dir = 'ltr';
    }

    allLangElements.forEach(el => {
      if (lang === 'fr' && el.dataset.langFr) el.textContent = el.dataset.langFr;
      else if (lang === 'en' && el.dataset.langEn) el.textContent = el.dataset.langEn;
      else if (lang === 'ar' && el.dataset.langAr) el.textContent = el.dataset.langAr;

      // placeholders
      if (el.placeholder) {
        if (lang === 'fr' && el.dataset.placeholderFr) el.placeholder = el.dataset.placeholderFr;
        else if (lang === 'en' && el.dataset.placeholderEn) el.placeholder = el.dataset.placeholderEn;
        else if (lang === 'ar' && el.dataset.placeholderAr) el.placeholder = el.dataset.placeholderAr;
      }
    });

    localStorage.setItem('preferredLang', lang);
  }
  // Init language
  const savedLang = localStorage.getItem('preferredLang') || 'fr';
  langSelect.value = savedLang;
  updateLanguage(savedLang);
  langSelect.addEventListener('change', (e) => {
    updateLanguage(e.target.value);
  });

  // === Thème sombre/claire toggle ===
  const themeToggleBtn = document.getElementById('theme-toggle');
  const body = document.body;

  function setTheme(theme) {
    if(theme === 'dark') {
      body.classList.add('dark-theme');
      themeToggleBtn.textContent = '☀️';
    } else {
      body.classList.remove('dark-theme');
      themeToggleBtn.textContent = '🌙';
    }
    localStorage.setItem('preferredTheme', theme);
  }
  const savedTheme = localStorage.getItem('preferredTheme') || 'light';
  setTheme(savedTheme);

  themeToggleBtn.addEventListener('click', () => {
    if(body.classList.contains('dark-theme')) setTheme('light');
    else setTheme('dark');
  });

  // === Carte choroplèthe simple avec Leaflet ===

  // Exemple de données taux suicide (par 100 000) simplifiées, en GeoJSON style
  // Source OMS données publiques (approximatives)
  // Ici on crée un GeoJSON simplifié (quelques pays seulement)

  const suicideRates = {
    "type": "FeatureCollection",
    "features": [
      {
        "type": "Feature",
        "properties": { "name": "Morocco", "rate": 3.9 },
        "geometry": {
          "type": "Point",
          "coordinates": [-7.0926, 31.7917]
        }
      },
      {
        "type": "Feature",
        "properties": { "name": "France", "rate": 12.1 },
        "geometry": {
          "type": "Point",
          "coordinates": [2.2137, 46.2276]
        }
      },
      {
        "type": "Feature",
        "properties": { "name": "United States", "rate": 14.5 },
        "geometry": {
          "type": "Point",
          "coordinates": [-95.7129, 37.0902]
        }
      },
      {
        "type": "Feature",
        "properties": { "name": "India", "rate": 16.5 },
        "geometry": {
          "type": "Point",
          "coordinates": [78.9629, 20.5937]
        }
      },
      {
        "type": "Feature",
        "properties": { "name": "Brazil", "rate": 6.2 },
        "geometry": {
          "type": "Point",
          "coordinates": [-51.9253, -14.2350]
        }
      },
      {
        "type": "Feature",
        "properties": { "name": "South Africa", "rate": 13.0 },
        "geometry": {
          "type": "Point",
          "coordinates": [22.9375, -30.5595]
        }
      },
      {
        "type": "Feature",
        "properties": { "name": "Russia", "rate": 25.0 },
        "geometry": {
          "type": "Point",
          "coordinates": [105.3188, 61.5240]
        }
      }
    ]
  };

  // Color scale fonction
  function getColor(rate) {
    return rate > 20 ? '#800026' :
           rate > 15 ? '#BD0026' :
           rate > 10 ? '#E31A1C' :
           rate > 5  ? '#FC4E2A' :
           rate > 0  ? '#FD8D3C' :
                       '#FFEDA0';
  }

  // Initialise Leaflet map
  const map = L.map('map').setView([20, 10], 2);

  // Tiles
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution:
      '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
  }).addTo(map);

  // Markers group
  const markersGroup = L.layerGroup().

