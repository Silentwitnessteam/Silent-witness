<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Silent Witness</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins&family=Cairo&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.3/dist/leaflet.css" />
  <style>
    :root {
      --color-bg-light: #ffffff;
      --color-text-light: #1c5980;
      --color-bg-dark: #1c1c1c;
      --color-text-dark: #f0f0f0;
      --primary-color: #204d7a;
      --accent-color: #8fc1a1;
    }
    body {
      margin: 0;
      font-family: 'Poppins', 'Cairo', sans-serif;
      background-color: var(--color-bg-light);
      color: var(--color-text-light);
      transition: background-color 0.3s ease, color 0.3s ease;
      min-height: 100vh;
      line-height: 1.5;
    }
    body.dark-theme {
      background-color: var(--color-bg-dark);
      color: var(--color-text-dark);
    }
    header {
      background: var(--primary-color);
      color: white;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 1rem;
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
    select.language-select {
      font-size: 1rem;
      padding: 0.3rem 0.6rem;
      border-radius: 5px;
      border: none;
      cursor: pointer;
    }
    button#theme-toggle {
      font-size: 1.4rem;
      background: transparent;
      border: none;
      cursor: pointer;
      color: white;
      user-select: none;
      transition: color 0.3s ease;
    }
    button#theme-toggle:hover {
      color: var(--accent-color);
    }
    .animated-text {
      font-size: 2rem;
      font-weight: 700;
      text-align: center;
      margin: 2rem 1rem 1rem;
      animation: pulseText 2s infinite;
    }
    @keyframes pulseText {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.7; transform: scale(1.05); }
    }
    main {
      max-width: 900px;
      margin: 0 auto 3rem;
      padding: 0 1rem;
    }
    section {
      margin-bottom: 3rem;
    }
    h2 {
      color: var(--primary-color);
      font-weight: 700;
      margin-bottom: 1rem;
      font-size: 1.5rem;
      border-bottom: 2px solid var(--accent-color);
      padding-bottom: 0.25rem;
    }
    p, ul, ol {
      font-size: 1.1rem;
    }
    ul, ol {
      padding-left: 1.5rem;
    }
    ul li, ol li {
      margin-bottom: 0.6rem;
    }
    a.download-btn {
      display: inline-block;
      background: var(--primary-color);
      color: white;
      padding: 0.7rem 1.5rem;
      border-radius: 8px;
      font-weight: 700;
      text-decoration: none;
      transition: background-color 0.3s ease, color 0.3s ease;
    }
    a.download-btn:hover {
      background: var(--accent-color);
      color: var(--primary-color);
    }
    #map {
      height: 450px;
      border-radius: 12px;
      box-shadow: 0 4px 8px rgb(0 0 0 / 0.15);
      margin-top: 1rem;
    }
    form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
    input, textarea {
      font-family: inherit;
      font-size: 1rem;
      padding: 0.7rem;
      border: 1px solid #ccc;
      border-radius: 6px;
      resize: vertical;
    }
    input:focus, textarea:focus {
      outline: 2px solid var(--primary-color);
      border-color: var(--primary-color);
    }
    button[type="submit"] {
      background-color: var(--primary-color);
      color: white;
      border: none;
      padding: 0.9rem;
      font-weight: 700;
      font-size: 1rem;
      border-radius: 6px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    button[type="submit"]:hover {
      background-color: var(--accent-color);
      color: var(--primary-color);
    }
    /* Donation buttons */
    .donation-section {
      text-align: center;
    }
    .donate-buttons {
      display: flex;
      justify-content: center;
      gap: 1.5rem;
      margin-top: 1rem;
      flex-wrap: wrap;
    }
    .donate-buttons a {
      background-color: var(--primary-color);
      color: white;
      padding: 0.8rem 1.8rem;
      border-radius: 8px;
      font-weight: 700;
      font-size: 1.1rem;
      text-decoration: none;
      transition: background-color 0.3s ease, color 0.3s ease;
      min-width: 140px;
      text-align: center;
    }
    .donate-buttons a:hover {
      background-color: var(--accent-color);
      color: var(--primary-color);
    }
    /* Dark mode fixes */
    body.dark-theme a.download-btn,
    body.dark-theme .donate-buttons a,
    body.dark-theme button[type="submit"] {
      color: #fff;
    }
    body.dark-theme input, body.dark-theme textarea {
      background-color: #333;
      color: #eee;
      border-color: #555;
    }
  </style>
  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script src="https://unpkg.com/leaflet@1.9.3/dist/leaflet.js"></script>
  <script>
    const translations = {
      fr: {
        title: "Vous n'êtes pas seul",
        whitepaper: "📘 Télécharger notre White Paper",
        whitepaperDesc: "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.",
        mapTitle: "Carte mondiale des suicides",
        statsTitle: "Statistiques clés",
        statsList: [
          "Près de 800 000 personnes se suicident chaque année (OMS)",
          "1 suicide toutes les 40 secondes dans le monde",
          "Le suicide est la 2e cause de mortalité chez les 15-29 ans"
        ],
        stepsTitle: "Étapes de détection IA",
        stepsList: [
          "Analyse des mots clés dans les messages, requêtes IA ou recherches web",
          "Corrélation des données vocales, textuelles ou comportementales",
          "Évaluation automatique du niveau de détresse",
          "Classement de l’urgence (vert / orange / rouge)",
          "Déclenchement d'une alerte vers ONG, autorités ou hôpitaux selon le niveau"
        ],
        donationTitle: "Soutenez Silent Witness",
        donationText: `Votre soutien est vital pour concrétiser ce projet humain et sauver des vies.\n\nChaque don contribue à améliorer la détection et l'assistance aux personnes en détresse.\n\nMerci de votre générosité !`,
        donatePaypal: "Faire un don via PayPal",
        donateStripe: "Faire un don via Stripe",
        contactTitle: "Contactez-nous",
        inputName: "Votre nom",
        inputEmail: "Votre email",
        inputMessage: "Votre message",
        submitBtn: "Envoyer",
        emailSuccess: "Message envoyé ! Merci pour votre contact.",
        emailError: "Erreur lors de l’envoi : "
      },
      en: {
        title: "You're not alone",
        whitepaper: "📘 Download our White Paper",
        whitepaperDesc: "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable.",
        mapTitle: "World Suicide Map",
        statsTitle: "Key Statistics",
        statsList: [
          "Nearly 800,000 people die by suicide every year (WHO)",
          "1 suicide every 40 seconds worldwide",
          "Suicide is the 2nd leading cause of death among 15-29 year olds"
        ],
        stepsTitle: "AI Detection Steps",
        stepsList: [
          "Analyze keywords in messages, AI queries or web searches",
          "Correlate vocal, textual or behavioral data",
          "Automatically evaluate distress level",
          "Classify urgency (green / orange / red)",
          "Trigger alert to NGOs, authorities or hospitals based on level"
        ],
        donationTitle: "Support Silent Witness",
        donationText: `Your support is vital to realize this human project and save lives.\n\nEvery donation helps improve detection and assistance to people in distress.\n\nThank you for your generosity!`,
        donatePaypal: "Donate via PayPal",
        donateStripe: "Donate via Stripe",
        contactTitle: "Contact Us",
        inputName: "Your name",
        inputEmail: "Your email",
        inputMessage: "Your message",
        submitBtn: "Send",
        emailSuccess: "Message sent! Thank you for reaching out.",
        emailError: "Error sending message: "
      },
      ar: {
        title: "لست وحدك",
        whitepaper: "📘 تحميل الورقة البيضاء",
        whitepaperDesc: "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر.",
        mapTitle: "خريطة الانتحار العالمية",
        statsTitle: "إحصائيات رئيسية",
        statsList: [
          "ما يقرب من 800,000 شخص ينتحرون كل عام (منظمة الصحة العالمية)",
          "انتحار واحد كل 40 ثانية في جميع أنحاء العالم",
          "الانتحار هو السبب الثاني للوفاة بين الشباب من 15 إلى 29 عامًا"
        ],
        stepsTitle: "خطوات الكشف بواسطة الذكاء الاصطناعي",
        stepsList: [
          "تحليل الكلمات المفتاحية في الرسائل، استفسارات الذكاء الاصطناعي أو البحث على الويب",
          "ربط البيانات الصوتية، النصية أو السلوكية",
          "التقييم التلقائي لمستوى الضيق",
          "تصنيف مستوى الطوارئ (أخضر / برتقالي / أحمر)",
          "إطلاق تنبيه للمنظمات، السلطات أو المستشفيات حسب المستوى"
        ],
        donationTitle: "ادعم Silent Witness",
        donationText: `دعمك حيوي لتحقيق هذا المشروع الإنساني وإنقاذ الأرواح.\n\nكل تبرع يساعد في تحسين الكشف والمساعدة للأشخاص في الضيق.\n\nشكرًا لكرمك!`,
        donatePaypal: "تبرع عبر PayPal",
        donateStripe: "تبرع عبر Stripe",
        contactTitle: "اتصل بنا",
        inputName: "اسمك",
        inputEmail: "بريدك الإلكتروني",
        inputMessage: "رسالتك",
        submitBtn: "إرسال",
        emailSuccess: "تم إرسال الرسالة! شكرًا لتواصلك معنا.",
        emailError: "خطأ في الإرسال: "
      }
    };

    function updateLanguage(lang) {
      document.querySelector('.animated-text').textContent = translations[lang].title;
      document.getElementById('wp-paragraph').textContent = translations[lang].whitepaperDesc;
      document.getElementById('wp-btn').textContent = translations[lang].whitepaper;
      document.getElementById('wp-btn').setAttribute('aria-label', translations[lang].whitepaper);
      document.getElementById('map-title').textContent = translations[lang].mapTitle;
      document.getElementById('stats-title').textContent = translations[lang].statsTitle;
      document.getElementById('steps-title').textContent = translations[lang].stepsTitle;
      document.getElementById('donation-title').textContent = translations[lang].donationTitle;
      document.getElementById('donation-text').textContent = translations[lang].donationText;
      document.getElementById('donate-paypal').textContent = translations[lang].donatePaypal;
      document.getElementById('donate-stripe').textContent = translations[lang].donateStripe;
      document.getElementById('contact-title').textContent = translations[lang].contactTitle;
      document.getElementById('input-name').placeholder = translations[lang].inputName;
      document.getElementById('input-email').placeholder = translations[lang].inputEmail;
      document.getElementById('input-message').placeholder = translations[lang].inputMessage;
      document.getElementById('form-submit').textContent = translations[lang].submitBtn;

      // update stats list
      const statsList = document.getElementById('stats-list');
      statsList.innerHTML = '';
      translations[lang].statsList.forEach(item => {
        const li = document.createElement('li');
        li.textContent = item;
        statsList.appendChild(li);
      });

      // update steps list
      const stepsList = document.getElementById('steps-list');
      stepsList.innerHTML = '';
      translations[lang].stepsList.forEach(item => {
        const li = document.createElement('li');
        li.textContent = item;
        stepsList.appendChild(li);
      });
    }

    // Dark mode toggle
    function toggleTheme() {
      document.body.classList.toggle('dark-theme');
    }

    // EmailJS send function
    function sendEmail(e) {
      e.preventDefault();
      const btn = document.getElementById('form-submit');
      btn.disabled = true;
      emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', e.target)
        .then(() => {
          alert(translations[document.getElementById('lang-select').value].emailSuccess);
          e.target.reset();
          updateLanguage(document.getElementById('lang-select').value);
          btn.disabled = false;
        })
        .catch((error) => {
          alert(translations[document.getElementById('lang-select').value].emailError + error.text);
          btn.disabled = false;
          updateLanguage(document.getElementById('lang-select').value);
        });
    }

    // Initialize Leaflet map with dummy suicide data by continent (per 100k)
    function initMap() {
      const map = L.map('map').setView([20, 0], 2);

      // Add OpenStreetMap tile layer
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 5,
        attribution: '&copy; OpenStreetMap contributors'
      }).addTo(map);

      // Example suicide data (rate per 100k inhabitants approx)
      const suicideData = [
        { continent: "Africa", coords: [1.6508, 10.2679], rate: 10 },
        { continent: "Asia", coords: [34.0479, 100.6197], rate: 12 },
        { continent: "Europe", coords: [54.5260, 15.2551], rate: 14 },
        { continent: "North America", coords: [54.5260, -105.2551], rate: 13 },
        { continent: "South America", coords: [-14.2350, -51.9253], rate: 9 },
        { continent: "Oceania", coords: [-22.7359, 140.0188], rate: 11 }
      ];

      suicideData.forEach(({ continent, coords, rate }) => {
        L.circle(coords, {
          color: 'red',
          fillColor: '#f03',
          fillOpacity: 0.5,
          radius: rate * 20000
        }).addTo(map)
          .bindPopup(`<strong>${continent}</strong><br>Taux de suicide : ${rate} pour 100k habitants`);
      });
    }

    window.addEventListener('DOMContentLoaded', () => {
      emailjs.init('_pR14KMi1syThzlmY');
      document.getElementById('contact-form').addEventListener('submit', sendEmail);
      document.getElementById('lang-select').addEventListener('change', e => updateLanguage(e.target.value));
      document.getElementById('theme-toggle').addEventListener('click', toggleTheme);
      updateLanguage('fr');
      initMap();
    });
  </script>
</head>
<body>
  <header>
    <h1>Silent Witness</h1>
    <div class="controls" role="region" aria-label="Contrôles de langue et thème">
      <label for="lang-select" class="visually-hidden">Choisir la langue</label>
      <select id="lang-select" class="language-select" aria-live="polite" aria-label="Choisir la langue">
        <option value="fr">Français</option>
        <option value="en">English</option>
        <option value="ar">العربية</option>
      </select>
      <button id="theme-toggle" aria-label="Basculer thème clair/sombre" title="Basculer thème clair/sombre">🌓</button>
    </div>
  </header>

  <div class="animated-text" aria-live="polite"></div>

  <main>
    <section aria-label="Description du projet">
      <p id="wp-paragraph"></p>
      <a id="wp-btn" href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf" target="_blank" rel="noopener noreferrer" class="download-btn"></a>
    </section>

    <section aria-label="Carte mondiale des suicides">
      <h2 id="map-title"></h2>
      <div id="map" role="region" aria-label="Carte interactive des taux de suicide par continent"></div>
    </section>

    <section aria-label="Statistiques clés">
      <h2 id="stats-title"></h2>
      <ul id="stats-list"></ul>
    </section>

    <section aria-label="Étapes de détection IA">
      <h2 id="steps-title"></h2>
      <ol id="steps-list"></ol>
    </section>

    <section class="donation-section" aria-label="Section de donation">
      <h2 id="donation-title"></h2>
      <p id="donation-text" style="white-space: pre-line;"></p>
      <div class="donate-buttons">
        <a href="https://www.paypal.com/donate?hosted_button_id=EXEMPLEID" target="_blank" rel="noopener noreferrer" id="donate-paypal" aria-label="Faire un don via PayPal"></a>
        <a href="https://buy.stripe.com/test_14k4gD2nYb7I7e4aEE" target="_blank" rel="noopener noreferrer" id="donate-stripe" aria-label="Faire un don via Stripe"></a>
      </div>
    </section>

    <section aria-label="Formulaire de contact">
      <h2 id="contact-title"></h2>
      <form id="contact-form">
        <input type="text" name="nom" id="input-name" placeholder="" required aria-required="true" />
        <input type="email" name="email" id="input-email" placeholder="" required aria-required="true" />
        <textarea name="message" id="input-message" rows="4" placeholder="" required aria-required="true"></textarea>
        <button type="submit" id="form-submit"></button>
      </form>
    </section>
  </main>

  <script>
    // Visually hidden class for accessibility (label)
    const style = document.createElement('style');
    style.textContent = `.visually-hidden {
      position: absolute !important;
      height: 1px; width: 1px;
      overflow: hidden;
      clip: rect(1px,1px,1px,1px);
      white-space: nowrap;
    }`;
    document.head.appendChild(style);
  </script>
</body>
</html>

