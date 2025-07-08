<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Silent Witness</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Poppins&family=Cairo&display=swap');

    :root {
      --color-bg-light: #ffffff;
      --color-text-light: #1c5980;
      --color-bg-dark: #1c1c1c;
      --color-text-dark: #f0f0f0;
      --color-primary: #1c5980;
      --color-primary-hover: #8fc1a1;
      --transition-speed: 0.3s;
    }
    body {
      margin: 0;
      font-family: 'Poppins', 'Cairo', sans-serif;
      background-color: var(--color-bg-light);
      color: var(--color-text-light);
      transition: background-color var(--transition-speed), color var(--transition-speed);
      line-height: 1.5;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 0 1rem;
    }
    body.dark-theme {
      background-color: var(--color-bg-dark);
      color: var(--color-text-dark);
    }
    header {
      width: 100%;
      max-width: 900px;
      padding: 1rem;
      background-color: var(--color-primary);
      color: white;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-sizing: border-box;
      border-radius: 8px;
      margin: 1rem 0;
    }
    h1 {
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
      padding: 0.4rem 0.6rem;
      border-radius: 6px;
      border: none;
      font-size: 1rem;
      cursor: pointer;
    }
    button#theme-toggle {
      background: transparent;
      border: 2px solid white;
      border-radius: 50%;
      color: white;
      font-size: 1.3rem;
      width: 36px;
      height: 36px;
      cursor: pointer;
      transition: background-color var(--transition-speed), color var(--transition-speed);
      display: flex;
      justify-content: center;
      align-items: center;
      user-select: none;
    }
    button#theme-toggle:hover {
      background-color: white;
      color: var(--color-primary);
    }

    .animated-text {
      font-size: 2.5rem;
      font-weight: 700;
      margin: 2rem auto;
      text-align: center;
      max-width: 900px;
      animation: pulseText 2.5s infinite;
      user-select: none;
    }
    @keyframes pulseText {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.6; transform: scale(1.05); }
    }
    main {
      width: 100%;
      max-width: 900px;
      box-sizing: border-box;
    }
    section {
      margin-bottom: 3rem;
      background: rgba(255 255 255 / 0.85);
      border-radius: 10px;
      padding: 1.8rem 1.5rem;
      box-shadow: 0 2px 8px rgb(0 0 0 / 0.1);
      transition: background var(--transition-speed), color var(--transition-speed);
    }
    body.dark-theme section {
      background: rgba(28 28 28 / 0.85);
      box-shadow: 0 2px 12px rgb(255 255 255 / 0.1);
    }
    section h2 {
      font-size: 1.6rem;
      margin-top: 0;
      margin-bottom: 1rem;
      font-weight: 600;
      color: var(--color-primary);
    }
    p, ul, ol {
      font-size: 1rem;
      margin-top: 0;
      margin-bottom: 1rem;
    }
    ul, ol {
      padding-left: 1.4rem;
    }
    ul li, ol li {
      margin-bottom: 0.5rem;
    }
    a.download-btn {
      display: inline-block;
      background-color: var(--color-primary);
      color: white;
      padding: 0.8rem 1.5rem;
      border-radius: 8px;
      text-decoration: none;
      font-weight: 600;
      transition: background-color var(--transition-speed), color var(--transition-speed);
      user-select: none;
    }
    a.download-btn:hover,
    a.download-btn:focus {
      background-color: var(--color-primary-hover);
      color: var(--color-primary);
      outline: none;
    }
    iframe {
      width: 100%;
      height: 500px;
      border: none;
      border-radius: 8px;
      margin-top: 1rem;
    }
    form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      margin-top: 1rem;
    }
    input, textarea {
      font-family: inherit;
      font-size: 1rem;
      padding: 0.8rem;
      border-radius: 6px;
      border: 1.5px solid #ccc;
      transition: border-color 0.3s;
      resize: vertical;
    }
    input:focus, textarea:focus {
      outline: none;
      border-color: var(--color-primary);
      box-shadow: 0 0 6px var(--color-primary);
    }
    button[type="submit"] {
      background-color: var(--color-primary);
      color: white;
      padding: 0.9rem;
      border: none;
      border-radius: 8px;
      font-size: 1.1rem;
      font-weight: 700;
      cursor: pointer;
      transition: background-color 0.3s;
      user-select: none;
    }
    button[type="submit"]:hover {
      background-color: var(--color-primary-hover);
      color: var(--color-primary);
    }
    /* Donation section styles */
    .donation-section {
      text-align: center;
      background: #e6f1ec;
      border-radius: 10px;
      padding: 1.8rem 1.5rem;
      box-shadow: 0 2px 8px rgb(0 0 0 / 0.05);
      margin-bottom: 3rem;
      transition: background var(--transition-speed), color var(--transition-speed);
    }
    body.dark-theme .donation-section {
      background: #2e443a;
      box-shadow: 0 2px 10px rgb(255 255 255 / 0.1);
    }
    .donation-section h2 {
      color: #1c5980;
      font-weight: 700;
      margin-bottom: 1rem;
    }
    body.dark-theme .donation-section h2 {
      color: #8fc1a1;
    }
    .donation-section p {
      font-size: 1.1rem;
      margin-bottom: 1.5rem;
      max-width: 700px;
      margin-left: auto;
      margin-right: auto;
      color: #254f3f;
    }
    body.dark-theme .donation-section p {
      color: #a3c0a0;
    }
    .donate-buttons {
      display: flex;
      justify-content: center;
      gap: 1.5rem;
      flex-wrap: wrap;
    }
    .donate-buttons a {
      background-color: #1c5980;
      color: white;
      padding: 0.8rem 1.8rem;
      border-radius: 8px;
      font-weight: 700;
      text-decoration: none;
      transition: background-color 0.3s;
      user-select: none;
      min-width: 140px;
      text-align: center;
    }
    .donate-buttons a:hover,
    .donate-buttons a:focus {
      background-color: #8fc1a1;
      color: #1c5980;
      outline: none;
    }

    /* Responsive */
    @media (max-width: 600px) {
      .animated-text {
        font-size: 1.8rem;
      }
      section {
        padding: 1rem 1rem;
      }
      header {
        flex-direction: column;
        gap: 1rem;
        align-items: flex-start;
      }
      .controls {
        width: 100%;
        justify-content: flex-start;
      }
      .donate-buttons {
        flex-direction: column;
        gap: 1rem;
      }
    }
  </style>

  <!-- EmailJS SDK -->
  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>

  <script>
    emailjs.init('_pR14KMi1syThzlmY');

    // Traductions multilingues complètes
    const translations = {
      fr: {
        title: "Vous n'êtes pas seul",
        whitepaper: "📘 Télécharger notre White Paper",
        paragraph: "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.",
        worldMapTitle: "Carte mondiale des suicides",
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
        contactTitle: "Contact",
        formNamePlaceholder: "Votre nom",
        formEmailPlaceholder: "Votre email",
        formMessagePlaceholder: "Votre message",
        formSubmitButton: "Envoyer",
        donationTitle: "Soutenez Silent Witness — Faites la différence aujourd’hui",
        donationText: "Le développement, la maintenance et l’amélioration continue de Silent Witness nécessitent des ressources importantes. Votre soutien est essentiel pour :\n- Affiner les algorithmes et renforcer la précision.\n- Assurer une veille éthique et la protection des données.\n- Déployer le projet auprès des populations vulnérables.\n- Former les équipes partenaires (ONG, hôpitaux).\n\nChaque don, petit ou grand, rapproche Silent Witness d’un monde plus sûr et solidaire.\n\nMerci pour votre générosité.",
        donatePaypal: "Faire un don via PayPal",
        donateStripe: "Faire un don via Stripe"
      },
      en: {
        title: "You're not alone",
        whitepaper: "📘 Download our White Paper",
        paragraph: "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable.",
        worldMapTitle: "Worldwide Suicide Map",
        statsTitle: "Key Statistics",
        statsList: [
          "Nearly 800,000 people die by suicide each year (WHO)",
          "1 suicide every 40 seconds worldwide",
          "Suicide is the 2nd leading cause of death among 15-29 year olds"
        ],
        stepsTitle: "AI Detection Steps",
        stepsList: [
          "Analysis of keywords in messages, AI queries or web searches",
          "Correlation of vocal, textual, or behavioral data",
          "Automatic evaluation of distress levels",
          "Urgency classification (green / orange / red)",
          "Alert triggering to NGOs, authorities or hospitals depending on level"
        ],
        contactTitle: "Contact",
        formNamePlaceholder: "Your name",
        formEmailPlaceholder: "Your email",
        formMessagePlaceholder: "Your message",
        formSubmitButton: "Send",
        donationTitle: "Support Silent Witness — Make a difference today",
        donationText: "The development, maintenance and continuous improvement of Silent Witness require significant resources. Your support is essential to:\n- Refine algorithms and improve accuracy.\n- Ensure ethical monitoring and data protection.\n- Deploy the project to vulnerable populations.\n- Train partner teams (NGOs, hospitals).\n\nEvery donation, big or small, brings Silent Witness closer to a safer, more caring world.\n\nThank you for your generosity.",
        donatePaypal: "Donate via PayPal",
        donateStripe: "Donate via Stripe"
      },
      ar: {
        title: "لست وحدك",
        whitepaper: "📘 تحميل الورقة البيضاء",
        paragraph: "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر.",
        worldMapTitle: "خريطة الانتحار العالمية",
        statsTitle: "إحصائيات رئيسية",
        statsList: [
          "يموت حوالي 800,000 شخص من الانتحار سنويًا (منظمة الصحة العالمية)",
          "انتحار واحد كل 40 ثانية في جميع أنحاء العالم",
          "الانتحار هو السبب الثاني للوفاة بين الأعمار 15-29 سنة"
        ],
        stepsTitle: "خطوات الكشف بالذكاء الاصطناعي",
        stepsList: [
          "تحليل الكلمات المفتاحية في الرسائل، استفسارات الذكاء الاصطناعي أو البحث على الإنترنت",
          "الربط بين البيانات الصوتية، النصية أو السلوكية",
          "التقييم التلقائي لمستوى الضيق",
          "تصنيف حالة الطوارئ (أخضر / برتقالي / أحمر)",
          "إطلاق التنبيه تلقائيًا إلى المنظمات، السلطات أو المستشفيات حسب المستوى"
        ],
        contactTitle: "اتصل بنا",
        formNamePlaceholder: "الاسم",
        formEmailPlaceholder: "البريد الإلكتروني",
        formMessagePlaceholder: "رسالتك",
        formSubmitButton: "إرسال",
        donationTitle: "ادعم Silent Witness — وكن جزءًا من التغيير اليوم",
        donationText: "يتطلب تطوير وصيانة وتحسين Silent Witness موارد كبيرة. دعمك ضروري لـ:\n- تحسين الخوارزميات وزيادة الدقة.\n- ضمان الرقابة الأخلاقية وحماية البيانات.\n- نشر المشروع بين الفئات الأكثر ضعفًا.\n- تدريب فرق الشركاء (المنظمات، المستشفيات).\n\nكل تبرع، صغير أو كبير، يقرب Silent Witness من عالم أكثر أمانًا ورعاية.\n\nشكرًا لكرمكم.",
        donatePaypal: "تبرع عبر PayPal",
        donateStripe: "تبرع عبر Stripe"
      }
    };

    // Mise à jour du contenu selon langue choisie
    function updateLanguage(lang) {
      document.documentElement.lang = lang;
      // Texte animé
      document.querySelector('.animated-text').textContent = translations[lang].title;
      // White paper section
      document.getElementById('wp-paragraph').textContent = translations[lang].paragraph;
      const wpBtn = document.getElementById('wp-btn');
      wpBtn.textContent = translations[lang].whitepaper;
      wpBtn.setAttribute('aria-label', translations[lang].whitepaper);
      // Sections titles
      document.getElementById('map-title').textContent = translations[lang].worldMapTitle;
      document.getElementById('stats-title').textContent = translations[lang].statsTitle;
      document.getElementById('steps-title').textContent = translations[lang].stepsTitle;
      document.getElementById('contact-title').textContent = translations[lang].contactTitle;
      document.getElementById('donation-title').textContent = translations[lang].donationTitle;

      // Stats list
      const statsList = document.getElementById('stats-list');
      statsList.innerHTML = '';
      translations[lang].statsList.forEach(item => {
        const li = document.createElement('li');
        li.textContent = item;
        statsList.appendChild(li);
      });

      // Steps list
      const stepsList = document.getElementById('steps-list');
      stepsList.innerHTML = '';
      translations[lang].stepsList.forEach(item => {
        const li = document.createElement('li');
        li.textContent = item;
        stepsList.appendChild(li);
      });

      // Contact form placeholders & button
      document.getElementById('input-name').placeholder = translations[lang].formNamePlaceholder;
      document.getElementById('input-email').placeholder = translations[lang].formEmailPlaceholder;
      document.getElementById('input-message').placeholder = translations[lang].formMessagePlaceholder;
      document.getElementById('form-submit').textContent = translations[lang].formSubmitButton;

      // Donation text & buttons
      document.getElementById('donation-text').textContent = translations[lang].donationText;
      document.getElementById('donate-paypal').textContent = translations[lang].donatePaypal;
      document.getElementById('donate-stripe').textContent = translations[lang].donateStripe;
    }

    // Toggle dark mode
    function toggleTheme() {
      document.body.classList.toggle('dark-theme');
    }

    // EmailJS form send
    function sendEmail(e) {
      e.preventDefault();
      const btn = document.getElementById('form-submit');
      btn.disabled = true;
      btn.textContent = '...';

      emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', e.target)
        .then(() => {
          alert('Message envoyé ! Merci pour votre contact.');
          e.target.reset();
          updateLanguage(document.getElementById('lang-select').value);
          btn.disabled = false;
        })
        .catch((error) => {
          alert('Erreur lors de l’envoi : ' + error.text);
          btn.disabled = false;
          updateLanguage(document.getElementById('lang-select').value);
        });
    }

    // Initialisation à la charge
    window.addEventListener('DOMContentLoaded', () => {
      emailjs.init('_pR14KMi1syThzlmY');

      // Event listeners
      document.getElementById('contact-form').addEventListener('submit', sendEmail);
      document.getElementById('lang-select').addEventListener('change', e => updateLanguage(e.target.value));
      document.getElementById('theme-toggle').addEventListener('click', toggleTheme);

      updateLanguage('fr');
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
      <button id="theme-toggle" aria-label="Basculer thème clair / sombre" title="Basculer thème clair / sombre">🌓</button>
    </div>
  </header>

  <div class="animated-text" aria-live="polite" aria-atomic="true" role="heading" aria-level="2"></div>

  <main>
    <!-- White Paper -->
    <section aria-labelledby="wp-title" role="region" tabindex="0">
      <h2 id="wp-title" class="visually-hidden">White Paper</h2>
      <p id="wp-paragraph"></p>
      <a id="wp-btn" href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf" target="_blank" rel="noopener" class="download-btn" role="button" aria-label="Télécharger le White Paper"></a>
    </section>

    <!-- Carte mondiale des suicides -->
    <section aria-labelledby="map-title" role="region" tabindex="0">
      <h2 id="map-title"></h2>
      <iframe 
        src="https://ourworldindata.org/grapher/suicide-death-rate?tab=map" 
        title="Carte mondiale des taux de suicide" 
        allowfullscreen 
        loading="lazy" 
        referrerpolicy="no-referrer"
      ></iframe>
    </section>

    <!-- Statistiques clés -->
    <section aria-labelledby="stats-title" role="region" tabindex="0">
      <h2 id="stats-title"></h2>
      <ul id="stats-list" aria-live="polite"></ul>
    </section>

    <!-- Étapes détection IA -->
    <section aria-labelledby="steps-title" role="region" tabindex="0">
      <h2 id="steps-title"></h2>
      <ol id="steps-list" aria-live="polite"></ol>
    </section>

    <!-- Donation -->
    <section class="donation-section" aria-labelledby="donation-title" role="region" tabindex="0">
      <h2 id="donation-title"></h2>
      <p id="donation-text" style="white-space: pre-line;"></p>
      <div class="donate-buttons">
        <a href="https://www.paypal.com/donate?hosted_button_id=YOUR_PAYPAL_BUTTON_ID" target="_blank" rel="noopener" id="donate-paypal" role="button"></a>
        <a href="https://buy.stripe.com/test_XXXXXXXXXXXX" target="_blank" rel="noopener" id="donate-stripe" role="button"></a>
      </div>
    </section>

    <!-- Contact -->
    <section aria-labelledby="contact-title" role="region" tabindex="0">
      <h2 id="contact-title"></h2>
      <form id="contact-form" aria-label="Formulaire de contact Silent Witness">
        <input id="input-name" type="text" name="nom" required autocomplete="name" />
        <input id="input-email" type="email" name="email" required autocomplete="email" />
        <textarea id="input-message" name="message" rows="4" required></textarea>
        <button type="submit" id="form-submit"></button>
      </form>
    </section>
  </main>

  <style>
    /* For screen readers: hide but keep accessible */
    .visually-hidden {
      position: absolute !important;
      width: 1px; height: 1px;
      padding: 0; margin: -1px; overflow: hidden;
      clip: rect(0 0 0 0); border: 0;
    }
  </style>
</body>
</html>

