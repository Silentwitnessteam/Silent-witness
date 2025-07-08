<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Silent Witness</title>
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background-color: var(--bg-color, #ffffff);
      color: var(--text-color, #1c5980);
      transition: background 0.3s, color 0.3s;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .dark-theme {
      --bg-color: #1c1c1c;
      --text-color: #f0f0f0;
    }
    header {
      padding: 1rem;
      background: #204d7a;
      color: white;
      width: 100%;
      max-width: 900px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-sizing: border-box;
    }
    .language-select, .theme-toggle {
      margin-left: 10px;
      font-size: 1rem;
      padding: 5px 8px;
      border-radius: 4px;
      border: none;
      cursor: pointer;
    }
    .theme-toggle {
      background-color: #1c5980;
      color: white;
    }
    .animated-text {
      font-size: 2rem;
      font-weight: bold;
      text-align: center;
      margin: 2rem 1rem 1rem;
      animation: pulseText 2s infinite;
      min-height: 3rem;
    }
    @keyframes pulseText {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.6; transform: scale(1.05); }
    }
    main {
      max-width: 900px;
      width: 100%;
      padding: 1rem;
      box-sizing: border-box;
      flex-grow: 1;
    }
    section {
      margin-bottom: 2rem;
      padding: 1rem 1rem 1.5rem;
      border-radius: 8px;
      background-color: var(--section-bg, #f4f9f6);
      box-shadow: 0 2px 6px rgb(28 89 128 / 0.15);
    }
    .dark-theme section {
      --section-bg: #2a2a2a;
      background-color: var(--section-bg);
      box-shadow: 0 2px 6px rgb(240 240 240 / 0.1);
    }
    h2 {
      color: var(--text-color);
      margin-top: 0;
      margin-bottom: 0.8rem;
    }
    p, ul, ol {
      color: var(--text-color);
      margin-top: 0;
      line-height: 1.5;
    }
    ul, ol {
      padding-left: 1.4rem;
    }
    a.download-btn {
      display: inline-block;
      background: #1c5980;
      color: white;
      padding: 0.8rem 1.5rem;
      border-radius: 8px;
      text-decoration: none;
      font-weight: bold;
      transition: background-color 0.3s, color 0.3s;
      margin-top: 0.8rem;
    }
    a.download-btn:hover {
      background: #8fc1a1;
      color: #1c5980;
    }
    iframe {
      width: 100%;
      height: 400px;
      border: none;
      margin-top: 1rem;
    }
    form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      margin-top: 1rem;
    }
    input, textarea {
      padding: 0.8rem;
      border-radius: 6px;
      border: 1px solid #ccc;
      font-size: 1rem;
      width: 100%;
      box-sizing: border-box;
    }
    input:focus, textarea:focus {
      outline-color: #1c5980;
      border-color: #1c5980;
    }
    button.submit-btn {
      padding: 0.8rem;
      background: #204d7a;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 1rem;
      transition: background-color 0.3s;
    }
    button.submit-btn:hover {
      background: #1c5980;
    }
    /* Map container */
    #map {
      height: 500px;
      width: 100%;
      border-radius: 8px;
    }
    /* Responsive */
    @media (max-width: 600px) {
      .animated-text {
        font-size: 1.5rem;
      }
      header {
        flex-wrap: wrap;
      }
      .language-select, .theme-toggle {
        margin: 8px 5px 0 0;
      }
    }
  </style>

  <!-- Leaflet CSS -->
  <link
    rel="stylesheet"
    href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
    integrity="sha256-sA+e2Zb65+VZCjUaa1uXCjMQFS9Nn5oYo8g9JfUoA34="
    crossorigin=""
  />
  <!-- EmailJS SDK -->
  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <!-- Leaflet JS -->
  <script
    src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"
    integrity="sha256-o9N1j8Mk7R8C3LxG7nDw6b4R7m7JlH3dWusK5tDgnz8="
    crossorigin=""
  ></script>

  <script>
    // Initialisation EmailJS
    emailjs.init('_pR14KMi1syThzlmY');

    // Traductions dynamiques
    const translations = {
      fr: {
        title: "Vous n'êtes pas seul",
        whitepaper: "📘 Télécharger notre White Paper",
        paragraph:
          "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.",
        statsTitle: "Statistiques clés",
        statsList: [
          "Près de 800 000 personnes se suicident chaque année (OMS)",
          "1 suicide toutes les 40 secondes dans le monde",
          "Le suicide est la 2e cause de mortalité chez les 15-29 ans",
        ],
        detectionTitle: "Étapes de détection IA",
        detectionSteps: [
          "Analyse des mots clés dans les messages, requêtes IA ou recherches web",
          "Corrélation des données vocales, textuelles ou comportementales",
          "Évaluation automatique du niveau de détresse",
          "Classement de l’urgence (vert / orange / rouge)",
          "Déclenchement d'une alerte vers ONG, autorités ou hôpitaux selon le niveau",
        ],
        contactTitle: "Contact",
        contactName: "Votre nom",
        contactEmail: "Votre email",
        contactMessage: "Votre message",
        contactSend: "Envoyer",
        donationTitle: "Faire un don",
        donationText:
          "Chaque contribution aide Silent Witness à protéger des vies grâce à l'IA. Merci pour votre soutien 💙",
      },
      en: {
        title: "You're not alone",
        whitepaper: "📘 Download our White Paper",
        paragraph:
          "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable.",
        statsTitle: "Key Statistics",
        statsList: [
          "Nearly 800,000 people die by suicide each year (WHO)",
          "1 suicide every 40 seconds worldwide",
          "Suicide is the 2nd leading cause of death among 15-29 year olds",
        ],
        detectionTitle: "AI Detection Steps",
        detectionSteps: [
          "Analysis of keywords in messages, AI queries or web searches",
          "Correlation of vocal, textual or behavioral data",
          "Automated distress level assessment",
          "Urgency classification (green / orange / red)",
          "Alert triggered to NGOs, authorities or hospitals according to the level",
        ],
        contactTitle: "Contact",
        contactName: "Your name",
        contactEmail: "Your email",
        contactMessage: "Your message",
        contactSend: "Send",
        donationTitle: "Make a donation",
        donationText:
          "Every contribution helps Silent Witness protect lives through AI. Thank you for your support 💙",
      },
      ar: {
        title: "لست وحدك",
        whitepaper: "📘 تحميل الورقة البيضاء",
        paragraph:
          "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر.",
        statsTitle: "إحصائيات رئيسية",
        statsList: [
          "يقع حوالي 800,000 حالة انتحار سنويًا (منظمة الصحة العالمية)",
          "انتحار واحد كل 40 ثانية في جميع أنحاء العالم",
          "الانتحار هو السبب الثاني للوفاة بين سن 15-29",
        ],
        detectionTitle: "مراحل الكشف باستخدام الذكاء الاصطناعي",
        detectionSteps: [
          "تحليل الكلمات الرئيسية في الرسائل، استفسارات الذكاء الاصطناعي أو عمليات البحث على الويب",
          "الربط بين البيانات الصوتية، النصية أو السلوكية",
          "التقييم التلقائي لمستوى الضيق",
          "تصنيف الطوارئ (أخضر / برتقالي / أحمر)",
          "إطلاق تنبيه للمنظمات أو السلطات أو المستشفيات حسب المستوى",
        ],
        contactTitle: "اتصل بنا",
        contactName: "اسمك",
        contactEmail: "بريدك الإلكتروني",
        contactMessage: "رسالتك",
        contactSend: "إرسال",
        donationTitle: "التبرع",
        donationText: "كل مساهمة تساعد Silent Witness على حماية الأرواح باستخدام الذكاء الاصطناعي. شكراً لدعمكم 💙",
      },
    };

    // Met à jour le texte selon la langue sélectionnée
    function updateLanguage(lang) {
      // Texte animé
      document.querySelector(".animated-text").textContent = translations[lang].title;

      // White Paper
      document.getElementById("wp-paragraph").textContent = translations[lang].paragraph;
      document.getElementById("wp-btn").textContent = translations[lang].whitepaper;

      // Statistiques
      document.getElementById("stats-title").textContent = translations[lang].statsTitle;
      const statsList = document.getElementById("stats-list");
      statsList.innerHTML = "";
      translations[lang].statsList.forEach((item) => {
        const li = document.createElement("li");
        li.textContent = item;
        statsList.appendChild(li);
      });

      // Étapes détection
      document.getElementById("detection-title").textContent = translations[lang].detectionTitle;
      const detectionList = document.getElementById("detection-list");
      detectionList.innerHTML = "";
      translations[lang].detectionSteps.forEach((item) => {
        const li = document.createElement("li");
        li.textContent = item;
        detectionList.appendChild(li);
      });

      // Contact
      document.getElementById("contact-title").textContent = translations[lang].contactTitle;
      document.getElementById("input-name").placeholder = translations[lang].contactName;
      document.getElementById("input-email").placeholder = translations[lang].contactEmail;
      document.getElementById("input-message").placeholder = translations[lang].contactMessage;
      document.getElementById("btn-send").textContent = translations[lang].contactSend;

      // Donation
      document.getElementById("donation-title").textContent = translations[lang].donationTitle;
      document.getElementById("donation-text").textContent = translations[lang].donationText;
    }

    // Toggle mode sombre
    function toggleTheme() {
      document.body.classList.toggle("dark-theme");
    }

    // Envoi formulaire EmailJS
    function sendEmail(e) {
      e.preventDefault();
      emailjs
        .sendForm("service_za2pm5i", "template_mt5ycpk", e.target)
        .then(() => alert("Message envoyé!"))
        .catch((error) => alert("Erreur: " + error));
    }

    // Initialisation au chargement
    window.addEventListener("DOMContentLoaded", () => {
      document.getElementById("contact-form").addEventListener("submit", sendEmail);
      document.getElementById("lang-select").addEventListener("change", (e) =>
        updateLanguage(e.target.value)
      );
      document.getElementById("theme-toggle").addEventListener("click", toggleTheme);

      updateLanguage("fr");

      // Initialiser la carte Leaflet
      const suicideData = [
        { country: "France", lat: 46.2276, lng: 2.2137, rate: 12.1 },
        { country: "Japan", lat: 36.2048, lng: 138.2529, rate: 16.5 },
        { country: "USA", lat: 37.0902, lng: -95.7129, rate: 14.5 },
        { country: "Brazil", lat: -14.235, lng: -51.9253, rate: 6.3 },
        { country: "India", lat: 20.5937, lng: 78.9629, rate: 15.7 },
        { country: "Russia", lat: 61.524, lng: 105.3188, rate: 26.5 },
      ];

      const map = L.map("map").setView([20, 0], 2);

      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution: "© OpenStreetMap contributors",
      }).addTo(map);

      suicideData.forEach((country) => {
        const radius = country.rate * 20000;
        const color =
          country.rate > 20 ? "#b30000" : country.rate > 15 ? "#e67e00" : "#1c5980";
        L.circle([country.lat, country.lng], {
          color,
          fillColor: color,
          fillOpacity: 0.5,
          radius,
        })
          .addTo(map)
          .bindPopup(
            `<strong>${country.country}</strong><br>Taux de suicide: ${country.rate} / 100k`
          );
      });
    });
  </script>
</head>
<body>
  <header>
    <h1>Silent Witness</h1>
    <div>
      <select id="lang-select" class="language-select" aria-label="Choix de langue">
        <option value="fr">Français</option>
        <option value="en">English</option>
        <option value="ar">العربية</option>
      </select>
      <button id="theme-toggle" class="theme-toggle" aria-label="Changer thème clair/sombre">🌓</button>
    </div>
  </header>

  <div class="animated-text" aria-live="polite" aria-atomic="true"></div>

  <main>
    <section>
      <p id="wp-paragraph"></p>
      <a
        id="wp-btn"
        href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf"
        target="_blank"
        rel="noopener noreferrer"
        class="download-btn"
        aria-label="Télécharger le White Paper"
        >📘 Télécharger notre White Paper</a
      >
    </section>

    <section>
      <h2 id="stats-title">Statistiques clés</h2>
      <ul id="stats-list" aria-live="polite" aria-atomic="true"></ul>
    </section>

    <section>
      <h2 id="detection-title">Étapes de détection IA</h2>
      <ol id="detection-list"></ol>
    </section>

    <section>
      <h2 id="donation-title">Faire un don</h2>
      <p id="donation-text"></p>
      <!-- PayPal Button -->
      <div id="paypal-container-UTEPDMT9UCV2S"></div>
      <script
        src="https://www.paypal.com/sdk/js?client-id=BAAwNQmuQNtmwbB198XpnMFgJqBHvKNcvg138E9ddcIrNxHGCrGT2tvdVOyLaJTqde8dM-9e9ZglZUXS9A&components=hosted-buttons&disable-funding=venmo&currency=USD"
      ></script>
      <script>
        paypal.HostedButtons({
          hostedButtonId: "UTEPDMT9UCV2S",
        }).render("#paypal-container-UTEPDMT9UCV2S");
      </script>
    </section>

    <section>
      <h2>Carte mondiale des suicides</h2>
      <div id="map" role="region" aria-label="Carte interactive des taux de suicide"></div>
    </section>

    <section>
      <h2 id="contact-title">Contact</h2>
      <form id="contact-form" aria-label="Formulaire de contact">
        <input
          id="input-name"
          type="text"
          name="nom"
          placeholder="Votre nom"
          required
          aria-required="true"
        />
        <input
          id="input-email"
          type="email"
          name="email"
          placeholder="Votre email"
          required
          aria-required="true"
        />
        <textarea
          id="input-message"
          name="message"
          rows="4"
          placeholder="Votre message"
          required
          aria-required="true"
        ></textarea>
        <button type="submit" id="btn-send" class="submit-btn">Envoyer</button>
      </form>
    </section>
  </main>
</body>
</html>

