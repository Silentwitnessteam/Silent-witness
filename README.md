<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Silent Witness</title>

  <!-- Poppins font -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;700;900&display=swap" rel="stylesheet" />

  <!-- Leaflet CSS -->
  <link
    rel="stylesheet"
    href="https://unpkg.com/leaflet@1.9.3/dist/leaflet.css"
    integrity="sha256-sA+oR7paO8qdhxz7PhR8CX6sCFmqaeg3LZvCtmFM9nM="
    crossorigin=""
  />

  <style>
    /* === Insère ici tout le CSS modernisé que je t’ai donné === */
    :root {
      --color-primary: #1c5980;
      --color-secondary: #8fc1a1;
      --color-bg-light: #fefefe;
      --color-bg-dark: #121212;
      --color-text-light: #222222;
      --color-text-dark: #e0e0e0;
      --transition-speed: 0.35s;
      --border-radius: 12px;
      --box-shadow-light: 0 4px 15px rgba(28, 89, 128, 0.15);
      --box-shadow-dark: 0 4px 20px rgba(0, 0, 0, 0.6);
      --font-family: 'Poppins', sans-serif;
    }

    *, *::before, *::after {
      box-sizing: border-box;
    }

    body {
      margin: 0; padding: 0;
      font-family: var(--font-family);
      background-color: var(--color-bg-light);
      color: var(--color-text-light);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      transition: background-color var(--transition-speed), color var(--transition-speed);
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
    }

    body.dark-theme {
      background-color: var(--color-bg-dark);
      color: var(--color-text-dark);
    }

    header {
      background: var(--color-primary);
      color: white;
      padding: 1.25rem 2.5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: var(--box-shadow-light);
      border-bottom-left-radius: var(--border-radius);
      border-bottom-right-radius: var(--border-radius);
    }

    header .logo-container {
      display: flex;
      align-items: center;
      gap: 1.2rem;
    }

    header img.logo {
      height: 50px;
      border-radius: 8px;
      object-fit: contain;
      filter: drop-shadow(0 0 2px rgba(0,0,0,0.1));
    }

    header h1 {
      font-weight: 900;
      font-size: 2rem;
      margin: 0;
      letter-spacing: 1.2px;
    }

    header .controls {
      display: flex;
      align-items: center;
      gap: 1.2rem;
    }

    select#lang-select {
      padding: 0.4rem 0.75rem;
      font-size: 1rem;
      border-radius: var(--border-radius);
      border: none;
      cursor: pointer;
      background: white;
      color: var(--color-primary);
      box-shadow: 0 2px 8px rgba(28,89,128,0.15);
      transition: background-color 0.25s ease;
    }

    select#lang-select:hover, select#lang-select:focus {
      background-color: var(--color-secondary);
      color: white;
      outline: none;
    }

    button#theme-toggle {
      font-size: 1.6rem;
      background: transparent;
      border: none;
      color: white;
      cursor: pointer;
      transition: color 0.3s ease;
      padding: 0.2rem 0.5rem;
      border-radius: var(--border-radius);
    }

    button#theme-toggle:hover {
      color: var(--color-secondary);
      background-color: rgba(255 255 255 / 0.15);
    }

    #main-title-section {
      max-width: 900px;
      margin: 3rem auto 4rem;
      text-align: center;
      padding: 0 1rem;
    }

    #main-title-section h1 {
      font-size: 3.4rem;
      font-weight: 900;
      margin-bottom: 0.25rem;
      color: var(--color-primary);
      user-select: none;
      letter-spacing: 1.4px;
      text-shadow: 0 2px 4px rgba(28,89,128,0.2);
    }

    #animated-text {
      font-size: 2.8rem;
      font-weight: 700;
      color: var(--color-secondary);
      user-select: none;
      animation: pulseText 2.5s infinite ease-in-out;
      letter-spacing: 0.8px;
    }

    @keyframes pulseText {
      0%, 100% {
        opacity: 1;
        transform: scale(1);
      }
      50% {
        opacity: 0.6;
        transform: scale(1.05);
      }
    }

    #donation-section {
      max-width: 400px;
      background: var(--color-primary);
      color: white;
      border-radius: var(--border-radius);
      padding: 2rem 2.5rem;
      margin: 2.5rem auto 5rem;
      box-shadow: 0 10px 25px rgba(28,89,128,0.3);
      text-align: center;
      user-select: none;
      font-weight: 600;
      letter-spacing: 0.8px;
    }

    #donation-section h2 {
      margin-bottom: 1.5rem;
      font-size: 1.9rem;
    }

    #paypal-button-container {
      margin-top: 1.5rem;
    }

    #whitepaper-section {
      max-width: 900px;
      margin: 0 auto 4rem;
      padding: 0 2rem;
      text-align: center;
    }

    #whitepaper-section p {
      font-size: 1.2rem;
      margin-bottom: 1.25rem;
      max-width: 700px;
      margin-left: auto;
      margin-right: auto;
      line-height: 1.5;
      color: var(--color-text-light);
    }

    #whitepaper-btn {
      display: inline-block;
      background: var(--color-primary);
      color: white;
      padding: 1rem 2.2rem;
      font-weight: 700;
      border-radius: var(--border-radius);
      text-decoration: none;
      box-shadow: 0 6px 14px rgba(28,89,128,0.2);
      transition: background-color 0.35s ease, color 0.35s ease;
      user-select: none;
    }

    #whitepaper-btn:hover {
      background: var(--color-secondary);
      color: var(--color-primary);
      box-shadow: 0 8px 22px rgba(143,193,161,0.5);
    }

    #map-section {
      max-width: 1100px;
      margin: 3.5rem auto 5rem;
      padding: 0 1rem;
    }

    #map-section h2 {
      text-align: center;
      font-weight: 900;
      font-size: 2.2rem;
      margin-bottom: 1.25rem;
      user-select: none;
      letter-spacing: 1.2px;
      color: var(--color-primary);
      text-shadow: 0 1px 3px rgba(28,89,128,0.2);
    }

    #map {
      width: 100%;
      height: 550px;
      border-radius: 16px;
      box-shadow: var(--box-shadow-light);
      border: none;
    }

    #filter-buttons {
      text-align: center;
      margin-bottom: 1.5rem;
    }

    #filter-buttons button {
      background: var(--color-primary);
      color: white;
      border: none;
      margin: 0 0.3rem;
      padding: 0.7rem 1.3rem;
      font-weight: 700;
      border-radius: var(--border-radius);
      cursor: pointer;
      transition: background-color 0.35s ease, color 0.35s ease;
      user-select: none;
      box-shadow: 0 3px 10px rgba(28,89,128,0.2);
    }

    #filter-buttons button.active,
    #filter-buttons button:hover {
      background: var(--color-secondary);
      color: var(--color-primary);
      box-shadow: 0 5px 18px rgba(143,193,161,0.4);
    }

    #stats-section {
      max-width: 900px;
      margin: 0 auto 5rem;
      padding: 0 2rem;
    }

    #stats-section h2 {
      font-weight: 900;
      font-size: 2.2rem;
      margin-bottom: 1.5rem;
      user-select: none;
      text-align: center;
      color: var(--color-primary);
      letter-spacing: 1.2px;
    }

    #stats-section ul {
      list-style: none;
      max-width: 700px;
      margin-left: auto;
      margin-right: auto;
      font-size: 1.15rem;
      line-height: 1.7;
      padding-left: 0;
    }

    #stats-section ul li {
      position: relative;
      padding-left: 1.6rem;
      margin-bottom: 1rem;
      color: var(--color-text-light);
    }

    #stats-section ul li::before {
      content: '•';
      position: absolute;
      left: 0;
      top: 0;
      color: var(--color-secondary);
      font-size: 1.4rem;
      line-height: 1;
    }

    #detection-steps {
      max-width: 900px;
      margin: 0 auto 5rem;
      padding: 0 2rem;
    }

    #detection-steps h2 {
      font-weight: 900;
      font-size: 2.2rem;
      margin-bottom: 1.5rem;
      text-align: center;
      user-select: none;
      color: var(--color-primary);
      letter-spacing: 1.2px;
    }

    #detection-steps ol {
      max-width: 700px;
      margin-left: auto;
      margin-right: auto;
      font-size: 1.15rem;
      line-height: 1.7;
      padding-left: 0;
      counter-reset: step-counter;
    }

    #detection-steps ol li {
      margin-bottom: 1.3rem;
      position: relative;
      padding-left: 3rem;
      color: var(--color-text-light);
    }

    #detection-steps ol li::before {
      content: counter(step-counter);
      counter-increment: step-counter;
      position: absolute;
      left: 0;
      top: 0;
      background: var(--color-primary);
      color: white;
      width: 2.2rem;
      height: 2.2rem;
      border-radius: 50%;
      text-align: center;
      line-height: 2.2rem;
      font-weight: 900;
      box-shadow: 0 2px 8px rgba(28, 89, 128, 0.3);
      user-select: none;
      font-size: 1.2rem;
    }

    #contact-section {
      max-width: 600px;
      margin: 0 auto 4rem;
      padding: 0 1rem;
    }

    #contact-section h2 {
      font-weight: 900;
      font-size: 2.2rem;
      margin-bottom: 1.25rem;
      text-align: center;
      user-select: none;
      color: var(--color-primary);
      letter-spacing: 1.2px;
    }

    form#contact-form {
      display: flex;
      flex-direction: column;
      gap: 1.25rem;
    }

    form#contact-form input,
    form#contact-form textarea {
      padding: 1rem;
      border-radius: var(--border-radius);
      border: 1.5px solid #ccc;
      font-size: 1rem;
      font-family: inherit;
      transition: border-color 0.3s ease;
    }

    form#contact-form input:focus,
    form#contact-form textarea:focus {
      border-color: var(--color-primary);
      outline: none;
      box-shadow: 0 0 8px rgba(28,89,128,0.3);
    }

    form#contact-form button {
      background: var(--color-primary);
      color: white;
      font-weight: 700;
      padding: 1rem;
      border: none;
      border-radius: var(--border-radius);
      cursor: pointer;
      transition: background-color 0.35s ease, color 0.35s ease;
      box-shadow: 0 4px 15px rgba(28,89,128,0.25);
    }

    form#contact-form button:hover {
      background: var(--color-secondary);
      color: var(--color-primary);
      box-shadow: 0 6px 20px rgba(143,193,161,0.5);
    }

    @media (max-width: 700px) {
      #main-title-section h1 {
        font-size: 2.4rem;
      }
      #animated-text {
        font-size: 2rem;
      }
      #map {
        height: 400px;
      }
      header {
        flex-direction: column;
        gap: 1.2rem;
        padding: 1rem 1.5rem;
        border-radius: 0 0 var(--border-radius) var(--border-radius);
      }
      header .controls {
        gap: 0.8rem;
      }
    }

    html[lang="ar"] {
      direction: rtl;
    }

    html[lang="ar"] body {
      text-align: right;
    }

    html[lang="ar"] header {
      direction: rtl;
    }

    html[lang="ar"] #contact-section input,
    html[lang="ar"] #contact-section textarea {
      direction: rtl;
      text-align: right;
    }
  </style>
</head>
<body>
  <header>
    <div class="logo-container">
      <img src="https://cdn-icons-png.flaticon.com/512/2983/2983738.png" alt="Silent Witness Logo" class="logo" />
      <h1 id="site-title">Silent Witness</h1>
    </div>
    <div class="controls">
      <select id="lang-select" aria-label="Choisir la langue">
        <option value="fr" selected>Français</option>
        <option value="ar">العربية</option>
      </select>
      <button id="theme-toggle" aria-label="Basculer thème sombre/claire">🌙</button>
    </div>
  </header>

  <main>
    <section id="main-title-section">
      <h1 data-lang-fr="Silent Witness" data-lang-ar="الشاهد الصامت">Silent Witness</h1>
      <div id="animated-text" data-lang-fr="Détection. Compréhension. Action." data-lang-ar="الكشف. الفهم. التحرك.">Détection. Compréhension. Action.</div>
    </section>

    <section id="donation-section">
      <h2 data-lang-fr="Soutenez notre cause" data-lang-ar="ادعم قضيتنا">Soutenez notre cause</h2>
      <div id="paypal-button-container">
        <!-- Intégration PayPal -->
        <form action="https://www.paypal.com/donate" method="post" target="_blank" rel="noopener">
          <!-- Remplace "TON_EMAIL_PAYPAL" par ton email PayPal -->
          <input type="hidden" name="business" value="TON_EMAIL_PAYPAL" />
          <input type="hidden" name="no_recurring" value="0" />
          <input type="hidden" name="currency_code" value="EUR" />
          <button type="submit" style="background:#fff; color: var(--color-primary); border:none; padding:0.8rem 1.5rem; border-radius: 12px; font-weight:700; cursor:pointer; box-shadow: 0 4px 10px rgba(28,89,128,0.3); transition: background-color 0.3s ease;">
            <span data-lang-fr="Faire un don via PayPal" data-lang-ar="التبرع عبر باي بال">Faire un don via PayPal</span>
          </button>
        </form>
      </div>
    </section>

    <section id="whitepaper-section">
      <p data-lang-fr="Découvrez notre livre blanc complet expliquant notre démarche et technologie." data-lang-ar="اكتشف ورقتنا البيضاء التي تشرح منهجنا وتقنياتنا.">
        Découvrez notre livre blanc complet expliquant notre démarche et technologie.
      </p>
      <a
        href="https://example.com/whitepaper.pdf"
        id="whitepaper-btn"
        target="_blank"
        rel="noopener"
        data-lang-fr="Télécharger le Livre Blanc"
        data-lang-ar="تحميل الورقة البيضاء"
      >
        Télécharger le Livre Blanc
      </a>
    </section>

    <section id="map-section">
      <h2 data-lang-fr="Carte Interactive" data-lang-ar="الخريطة التفاعلية">Carte Interactive</h2>
      <div id="filter-buttons">
        <button class="active" data-filter="all" data-lang-fr="Tous" data-lang-ar="الكل">Tous</button>
        <button data-filter="support" data-lang-fr="Soutien" data-lang-ar="الدعم">Soutien</button>
        <button data-filter="intervention" data-lang-fr="Intervention" data-lang-ar="التدخل">Intervention</button>
      </div>
      <div id="map" aria-label="Carte interactive des points d'intervention"></div>
    </section>

    <section id="stats-section">
      <h2 data-lang-fr="Statistiques" data-lang-ar="الإحصائيات">Statistiques</h2>
      <ul>
        <li data-lang-fr="Plus de 10 000 cas détectés depuis 2023." data-lang-ar="تم الكشف عن أكثر من 10,000 حالة منذ عام 2023."></li>
        <li data-lang-fr="Interventions rapides dans plus de 50 régions." data-lang-ar="تدخلات سريعة في أكثر من 50 منطقة."></li>
        <li data-lang-fr="Taux de succès d’alerte à 92%." data-lang-ar="معدل نجاح التنبيه 92٪."></li>
      </ul>
    </section>

    <section id="detection-steps">
      <h2 data-lang-fr="Étapes de Détection" data-lang-ar="خطوات الكشف">Étapes de Détection</h2>
      <ol>
        <li data-lang-fr="Analyse vocale continue et discrète." data-lang-ar="تحليل صوتي مستمر وسري."></li>
        <li data-lang-fr="Détection des émotions et signaux d’alerte." data-lang-ar="الكشف عن العواطف وإشارات الإنذار."></li>
        <li data-lang-fr="Envoi d’alerte aux autorités compétentes." data-lang-ar="إرسال تنبيه للسلطات المختصة."></li>
        <li data-lang-fr="Assistance personnalisée 24/7." data-lang-ar="دعم شخصي على مدار الساعة."></li>
      </ol>
    </section>

    <section id="contact-section">
      <h2 data-lang-fr="Contactez-nous" data-lang-ar="اتصل بنا">Contactez-nous</h2>
      <form id="contact-form" action="mailto:tonemail@example.com" method="post" enctype="text/plain">
        <input type="text" name="name" placeholder="Nom" required data-placeholder-fr="Nom" data-placeholder-ar="الاسم" />
        <input type="email" name="email" placeholder="Email" required data-placeholder-fr="Email" data-placeholder-ar="البريد الإلكتروني" />
        <textarea name="message" rows="5" placeholder="Votre message" required data-placeholder-fr="Votre message" data-placeholder-ar="رسالتك"></textarea>
        <button type="submit" data-lang-fr="Envoyer" data-lang-ar="إرسال">Envoyer</button>
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
    // === Gestion langue simple (FR / AR) ===
    const langSelect = document.getElementById('lang-select');
    const allLangElements = document.querySelectorAll('[data-lang-fr]');

    function updateLanguage(lang) {
      // Change html lang and direction
      document.documentElement.lang = lang;
      if (lang === 'ar') {
        document.documentElement.dir = 'rtl';
      } else {
        document.documentElement.dir = 'ltr';
      }

      // Textes multi-langues
      allLangElements.forEach(el => {
        if (lang === 'ar') {
          if(el.dataset.langAr) el.textContent = el.dataset.langAr;
          if(el.dataset.placeholderAr) el.placeholder = el.dataset.placeholderAr;
        } else {
          if(el.dataset.langFr) el.textContent = el.dataset.langFr;
          if(el.dataset.placeholderFr) el.placeholder = el.dataset.placeholderFr;
        }
      });

      // Sauvegarde dans localStorage
      localStorage.setItem('preferredLang', lang);
    }

    // Initialiser langue au chargement
    const savedLang = localStorage.getItem('preferredLang') || 'fr';
    langSelect.value = savedLang;
    updateLanguage(savedLang);

    langSelect.addEventListener('change', (e) => {
      updateLanguage(e.target.value);
    });

    // === Gestion thème sombre/claire ===
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

    // Initialiser thème au chargement
    const savedTheme = localStorage.getItem('preferredTheme') || 'light';
    setTheme(savedTheme);

    themeToggleBtn.addEventListener('click', () => {
      if(body.classList.contains('dark-theme')) {
        setTheme('light');
      } else {
        setTheme('dark');
      }
    });

    // === Leaflet carte ===
    const map = L.map('map').setView([33.5731, -7.5898], 6); // Maroc centré

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution:
        '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
    }).addTo(map);

    // Exemple de markers avec catégorie
    const markersData = [
      {
        coords: [34.020882, -6.841650],
        title: {fr: 'Centre de Soutien Rabat', ar: 'مركز الدعم الرباط'},
        category: 'support',
      },
      {
        coords: [33.971590, -6.849813],
        title: {fr: 'Intervention Casablanca', ar: 'تدخل الدار البيضاء'},
        category: 'intervention',
      },
      {
        coords: [35.7595, -5.83395],
        title: {fr: 'Soutien Tanger', ar: 'دعم طنجة'},
        category: 'support',
      },
      {
        coords: [31.6295, -8.0089],
        title: {fr: 'Intervention Marrakech', ar: 'تدخل مراكش'},
        category: 'intervention',
      },
    ];

    // Création des marqueurs Leaflet
    const markers = markersData.map(({coords, title, category}) => {
      const marker = L.marker(coords).addTo(map);
      marker.bindPopup(`<strong>${title.fr}</strong>`);
      marker.category = category;
      return marker;
    });

    // Filtrage des marqueurs
    const filterButtons = document.querySelectorAll('#filter-buttons button');
    filterButtons.forEach(btn => {
      btn.addEventListener('click', () => {
        filterButtons.forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        const filter = btn.dataset.filter;
        markers.forEach(m => {
          if(filter === 'all' || m.category === filter) {
            if(!map.hasLayer(m)) map.addLayer(m);
          } else {
            if(map.hasLayer(m)) map.removeLayer(m);
          }
        });
      });
    });

    // Mise à jour popup langue sur changement de langue
    langSelect.addEventListener('change', (e) => {
      const lang = e.target.value;
      markers.forEach((m, i) => {
        const title = markersData[i].title[lang];
        m.getPopup().setContent(`<strong>${title}</strong>`);
      });
    });

  </script>
</body>
</html>
