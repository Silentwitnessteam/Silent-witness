<!DOCTYPE html>
<html lang="fr" dir="ltr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Silent Witness</title>

<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Cairo&family=Poppins:wght@400;700&display=swap" rel="stylesheet" />

<!-- Leaflet CSS -->
<link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />

<style>
  :root {
    --color-primary: #1c5980;
    --color-primary-light: #8fc1a1;
    --color-bg-light: #ffffff;
    --color-bg-dark: #1c1c1c;
    --color-text-light: #1c5980;
    --color-text-dark: #f0f0f0;
  }

  html, body {
    margin: 0; padding: 0; height: 100%;
    font-family: 'Poppins', sans-serif;
    background-color: var(--color-bg-light);
    color: var(--color-text-light);
    transition: background-color 0.3s, color 0.3s;
    scroll-behavior: smooth;
  }

  body.dark-theme {
    background-color: var(--color-bg-dark);
    color: var(--color-text-dark);
  }

  /* Force font Cairo & uniform size for Arabic */
  html[lang="ar"] body {
    font-family: 'Cairo', sans-serif !important;
    font-size: 16px !important;
    line-height: 1.5 !important;
  }

  header {
    background-color: var(--color-primary);
    color: white;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 1.5rem;
    box-shadow: 0 3px 8px rgba(0,0,0,0.2);
  }
  header h1 {
    margin: 0;
    font-weight: 700;
    font-size: 1.8rem;
  }
  .controls {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  select#lang-select {
    padding: 0.4rem 0.6rem;
    border-radius: 6px;
    border: none;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
  }
  button#theme-toggle {
    background: transparent;
    border: none;
    font-size: 1.6rem;
    cursor: pointer;
    color: white;
    padding: 0.2rem;
    transition: color 0.3s;
  }
  button#theme-toggle:hover {
    color: var(--color-primary-light);
  }

  main {
    max-width: 1000px;
    margin: 1rem auto 2rem;
    padding: 0 1rem;
  }

  /* Hero with relevant background image */
  .hero {
    background: url('https://images.unsplash.com/photo-1535223289827-42f1e9919769?auto=format&fit=crop&w=1350&q=80') no-repeat center center/cover;
    height: 280px;
    border-radius: 12px;
    box-shadow: 0 0 25px rgba(28,89,128,0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    text-shadow: 0 0 10px rgba(0,0,0,0.9);
    margin-bottom: 2rem;
  }

  /* Animated text - fixed size & uniform */
  .animated-text {
    font-family: 'Cairo', sans-serif;
    font-size: 2.8rem !important;
    font-weight: 700;
    line-height: 1.2;
    text-align: center;
    animation: fadePulse 3s ease-in-out infinite;
    max-width: 90%;
  }
  @keyframes fadePulse {
    0%,100% {opacity: 1; transform: scale(1);}
    50% {opacity: 0.6; transform: scale(1.05);}
  }

  section {
    margin-bottom: 2.5rem;
  }

  h2 {
    color: var(--color-primary);
    font-weight: 700;
    margin-bottom: 1rem;
    font-size: 1.8rem;
  }

  p, li {
    font-size: 1.1rem;
    line-height: 1.5;
  }

  ul, ol {
    padding-left: 1.4rem;
  }

  a.download-btn {
    display: inline-block;
    background: var(--color-primary);
    color: white;
    padding: 0.8rem 1.5rem;
    border-radius: 8px;
    font-weight: 700;
    text-decoration: none;
    transition: background-color 0.3s, color 0.3s;
    margin-top: 0.5rem;
  }
  a.download-btn:hover {
    background: var(--color-primary-light);
    color: var(--color-primary);
  }

  #map {
    height: 450px;
    width: 100%;
    border-radius: 12px;
    box-shadow: 0 0 20px rgba(28,89,128,0.3);
  }

  /* Contact form */
  form#contact-form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    max-width: 500px;
  }
  form#contact-form input,
  form#contact-form textarea {
    padding: 0.7rem 1rem;
    border-radius: 6px;
    border: 1px solid #ccc;
    font-size: 1rem;
    font-family: inherit;
  }
  form#contact-form textarea {
    resize: vertical;
  }
  form#contact-form button {
    background-color: var(--color-primary);
    color: white;
    font-weight: 700;
    padding: 0.8rem 0;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 1.1rem;
    transition: background-color 0.3s;
  }
  form#contact-form button:hover {
    background-color: var(--color-primary-light);
    color: var(--color-primary);
  }

  /* Paypal donation button */
  .paypal-btn {
    background-color: #ffc439;
    color: #111;
    font-weight: 700;
    padding: 0.8rem 1.5rem;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 1.1rem;
    box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    transition: background-color 0.3s ease;
  }
  .paypal-btn:hover {
    background-color: #ffb700;
  }

  footer {
    text-align: center;
    padding: 1rem;
    color: var(--color-primary);
    font-weight: 600;
    border-top: 1px solid var(--color-primary-light);
  }

  /* Responsive */
  @media (max-width: 600px) {
    header {
      flex-direction: column;
      gap: 1rem;
    }
    main {
      margin: 1rem 0 2rem;
      padding: 0 1rem;
      max-width: 100%;
    }
    form#contact-form {
      width: 100%;
      max-width: none;
    }
  }
</style>

<!-- Leaflet JS -->
<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>

<!-- EmailJS SDK -->
<script src="https://cdn.emailjs.com/dist/email.min.js"></script>

<script>
  // EmailJS init
  emailjs.init('_pR14KMi1syThzlmY');

  function sendEmail(e) {
    e.preventDefault();
    emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', e.target)
    .then(() => {
      alert(lang === 'fr' ? 'Message envoyé!' : (lang === 'en' ? 'Message sent!' : 'تم إرسال الرسالة!'));
      e.target.reset();
    })
    .catch(err => alert('Erreur: ' + err));
  }

  // Translations object
  const translations = {
    fr: {
      title: "Vous n'êtes pas seul",
      whitepaper: "📘 Télécharger notre White Paper",
      paragraph: "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.",
      mapTitle: "Carte mondiale des suicides",
      statsTitle: "Statistiques clés",
      statsList: [
        "Près de 800 000 personnes se suicident chaque année (OMS)",
        "1 suicide toutes les 40 secondes dans le monde",
        "Le suicide est la 2e cause de mortalité chez les 15-29 ans"
      ],
      detectionTitle: "Étapes de détection IA",
      detectionList: [
        "Analyse des mots clés dans les messages, requêtes IA ou recherches web",
        "Corrélation des données vocales, textuelles ou comportementales",
        "Évaluation automatique du niveau de détresse",
        "Classement de l’urgence (vert / orange / rouge)",
        "Déclenchement d'une alerte vers ONG, autorités ou hôpitaux selon le niveau"
      ],
      contactTitle: "Contact",
      contactSubmit: "Envoyer",
      donationTitle: "Soutenez Silent Witness",
      donationText: "Contribuez à concrétiser ce projet d’IA éthique en faisant un don. Chaque aide compte pour sauver des vies.",
      paypalBtn: "Faire un don via PayPal"
    },
    en: {
      title: "You're not alone",
      whitepaper: "📘 Download our White Paper",
      paragraph: "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable.",
      mapTitle: "World Suicide Rates Map",
      statsTitle: "Key Statistics",
      statsList: [
        "Nearly 800,000 people die by suicide annually (WHO)",
        "1 suicide every 40 seconds worldwide",
        "Suicide is the 2nd leading cause of death among 15-29 year olds"
      ],
      detectionTitle: "AI Detection Steps",
      detectionList: [
        "Analyze keywords in messages, AI queries, or web searches",
        "Correlate vocal, textual, or behavioral data",
        "Automatically assess distress level",
        "Urgency ranking (green / orange / red)",
        "Trigger alert to NGOs, authorities, or hospitals based on level"
      ],
      contactTitle: "Contact",
      contactSubmit: "Send",
      donationTitle: "Support Silent Witness",
      donationText: "Help bring this ethical AI project to life by making a donation. Every bit helps save lives.",
      paypalBtn: "Donate via PayPal"
    },
    ar: {
      title: "لست وحدك",
      whitepaper: "📘 تحميل الورقة البيضاء",
      paragraph: "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر.",
      mapTitle: "خريطة معدلات الانتحار العالمية",
      statsTitle: "إحصائيات رئيسية",
      statsList: [
        "يقع حوالي 800,000 حالة انتحار سنويًا (منظمة الصحة العالمية)",
        "انتحار واحد كل 40 ثانية في جميع أنحاء العالم",
        "الانتحار هو السبب الثاني للوفاة بين الأعمار 15-29 سنة"
      ],
      detectionTitle: "خطوات اكتشاف الذكاء الاصطناعي",
      detectionList: [
        "تحليل الكلمات المفتاحية في الرسائل، استعلامات الذكاء الاصطناعي أو عمليات البحث على الويب",
        "الربط بين البيانات الصوتية، النصية أو السلوكية",
        "التقييم التلقائي لمستوى الضيق",
        "تصنيف مستوى الطوارئ (أخضر / برتقالي / أحمر)",
        "إطلاق تنبيه للمنظمات أو السلطات أو المستشفيات حسب المستوى"
      ],
      contactTitle: "اتصل بنا",
      contactSubmit: "إرسال",
      donationTitle: "ادعم Silent Witness",
      donationText: "ساهم في تحقيق هذا المشروع الأخلاقي للذكاء الاصطناعي من خلال التبرع. كل مساعدة تُنقذ حياة.",
      paypalBtn: "التبرع عبر بايبال"
    }
  };

  let lang = 'fr';

  // Update UI texts on language change
  function updateLanguage(selectedLang) {
    lang = selectedLang;
    document.documentElement.lang = selectedLang;
    document.documentElement.dir = (selectedLang === 'ar') ? 'rtl' : 'ltr';

    document.querySelector('.animated-text').textContent = translations[lang].title;

    document.getElementById('wp-paragraph').textContent = translations[lang].paragraph;
    const wpBtn = document.getElementById('wp-btn');
    wpBtn.textContent = translations[lang].whitepaper;
    wpBtn.href = "https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf";

    document.getElementById('map-title').textContent = translations[lang].mapTitle;

    // Stats list
    const statsTitle = document.getElementById('stats-title');
    const statsList = document.getElementById('stats-list');
    statsTitle.textContent = translations[lang].statsTitle;
    statsList.innerHTML = '';
    translations[lang].statsList.forEach(item => {
      const li = document.createElement('li');
      li.textContent = item;
      statsList.appendChild(li);
    });

    // Detection steps
    const detectionTitle = document.getElementById('detection-title');
    const detectionList = document.getElementById('detection-list');
    detectionTitle.textContent = translations[lang].detectionTitle;
    detectionList.innerHTML = '';
    translations[lang].detectionList.forEach(item => {
      const li = document.createElement('li');
      li.textContent = item;
      detectionList.appendChild(li);
    });

    // Contact section
    document.getElementById('contact-title').textContent = translations[lang].contactTitle;
    document.getElementById('submit-btn').textContent = translations[lang].contactSubmit;

    // Donation section
    document.getElementById('donation-title').textContent = translations[lang].donationTitle;
    document.getElementById('donation-text').textContent = translations[lang].donationText;
    document.getElementById('paypal-donate-btn').textContent = translations[lang].paypalBtn;
  }

  function toggleTheme() {
    document.body.classList.toggle('dark-theme');
  }

  // Init Leaflet map simple, stable
  let map;
  window.onload = () => {
    document.getElementById('contact-form').addEventListener('submit', sendEmail);
    document.getElementById('lang-select').addEventListener('change', (e) => updateLanguage(e.target.value));
    document.getElementById('theme-toggle').addEventListener('click', toggleTheme);

    updateLanguage(lang);

    map = L.map('map').setView([20, 0], 2);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      maxZoom: 6,
      attribution: '&copy; OpenStreetMap contributors'
    }).addTo(map);
  };
</script>
</head>
<body>
<header>
  <h1>Silent Witness</h1>
  <div class="controls">
    <select id="lang-select" aria-label="Choisir la langue">
      <option value="fr">Français</option>
      <option value="en">English</option>
      <option value="ar">العربية</option>
    </select>
    <button id="theme-toggle" class="theme-toggle" aria-label="Basculer thème clair/sombre">🌓</button>
  </div>
</header>

<main>
  <section class="hero" role="banner" aria-label="Illustration du projet Silent Witness">
    <div class="animated-text" aria-live="polite" aria-atomic="true"></div>
  </section>

  <section aria-label="Présentation du projet">
    <p id="wp-paragraph"></p>
    <a id="wp-btn" class="download-btn" target="_blank" rel="noopener noreferrer" aria-label="Télécharger le white paper"></a>
  </section>

  <section aria-label="Carte mondiale des taux de suicide">
    <h2 id="map-title">Carte mondiale des suicides</h2>
    <div id="map" role="region" aria-label="Carte interactive des taux de suicide"></div>
  </section>

  <section aria-label="Statistiques clés sur le suicide">
    <h2 id="stats-title">Statistiques clés</h2>
    <ul id="stats-list" aria-live="polite" aria-atomic="true"></ul>
  </section>

  <section aria-label="Étapes de détection IA">
    <h2 id="detection-title">Étapes de détection IA</h2>
    <ol id="detection-list" aria-live="polite" aria-atomic="true"></ol>
  </section>

  <section aria-label="Formulaire de contact">
    <h2 id="contact-title">Contact</h2>
    <form id="contact-form" aria-describedby="contact-desc" novalidate>
      <input type="text" name="nom" placeholder="Votre nom" required aria-required="true" autocomplete="name" />
      <input type="email" name="email" placeholder="Votre email" required aria-required="true" autocomplete="email" />
      <textarea name="message" rows="4" placeholder="Votre message" required aria-required="true"></textarea>
      <button id="submit-btn" type="submit">Envoyer</button>
    </form>
  </section>

  <section aria-label="Section de donation">
    <h2 id="donation-title">Soutenez Silent Witness</h2>
    <p id="donation-text">Contribuez à concrétiser ce projet d’IA éthique en faisant un don. Chaque aide compte pour sauver des vies.</p>
    <!-- PayPal Donate Button -->
    <form action="https://www.paypal.com/donate" method="post" target="_blank" style="max-width: 220px;">
      <input type="hidden" name="hosted_button_id" value="UTEPDMT9UCV2S" />
      <button type="submit" class="paypal-btn" id="paypal-donate-btn" aria-label="Faire un don via PayPal">Faire un don via PayPal</button>
    </form>
  </section>
</main>

<footer>
  © 2025 Silent Witness. Tous droits réservés.
</footer>

</body>
</html>

