<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Silent Witness</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&family=Cairo&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    /* Reset */
    *, *::before, *::after {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      font-family: 'Poppins', 'Cairo', sans-serif;
      background-color: var(--bg-color, #f9fafd);
      color: var(--text-color, #1c5980);
      line-height: 1.5;
      transition: background-color 0.4s ease, color 0.4s ease;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }
    :root {
      --primary-color: #1c5980;
      --secondary-color: #8fc1a1;
      --bg-color: #f9fafd;
      --text-color: #1c5980;
      --btn-bg: var(--primary-color);
      --btn-hover-bg: var(--secondary-color);
      --input-border: #ccc;
      --input-focus: var(--primary-color);
    }
    .dark-theme {
      --bg-color: #1c1c1c;
      --text-color: #f0f0f0;
      --btn-bg: #8fc1a1;
      --btn-hover-bg: #1c5980;
      --input-border: #555;
      --input-focus: #8fc1a1;
      background-color: var(--bg-color);
      color: var(--text-color);
    }
    header {
      background: var(--primary-color);
      color: white;
      padding: 0.8rem 1.5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      font-size: 1rem;
    }
    header h1 {
      font-weight: 700;
      font-size: 1.5rem;
      margin: 0;
    }
    .controls {
      display: flex;
      gap: 0.8rem;
      align-items: center;
      flex-wrap: wrap;
    }
    select.language-select {
      padding: 0.3rem 0.5rem;
      font-size: 0.9rem;
      border-radius: 6px;
      border: none;
      cursor: pointer;
      font-weight: 600;
      min-width: 100px;
    }
    button#theme-toggle {
      background: transparent;
      border: 2px solid white;
      color: white;
      padding: 0.2rem 0.6rem;
      border-radius: 6px;
      font-size: 1.1rem;
      cursor: pointer;
      transition: background-color 0.3s ease, color 0.3s ease;
      user-select: none;
    }
    button#theme-toggle:hover {
      background: white;
      color: var(--primary-color);
    }

    main {
      flex: 1 0 auto;
      max-width: 850px;
      margin: 1.5rem auto 2rem;
      padding: 0 1rem;
      width: 100%;
      text-align: left;
    }
    .animated-text {
      font-weight: 700;
      font-size: 2rem;
      margin-bottom: 1.2rem;
      color: var(--primary-color);
      animation: pulseText 3s ease-in-out infinite;
      user-select: none;
      text-align: center;
    }
    @keyframes pulseText {
      0%, 100% {opacity: 1; transform: scale(1);}
      50% {opacity: 0.6; transform: scale(1.05);}
    }

    section {
      margin-bottom: 2rem;
    }
    section h2 {
      color: var(--primary-color);
      font-weight: 700;
      font-size: 1.3rem;
      margin-bottom: 0.8rem;
      border-bottom: 2px solid var(--secondary-color);
      padding-bottom: 0.1rem;
    }
    p, li {
      font-size: 1rem;
      margin-bottom: 0.5rem;
      color: var(--text-color);
    }
    ul, ol {
      padding-left: 1.1rem;
      color: var(--text-color);
    }

    /* Download Button */
    .download-btn {
      display: inline-block;
      padding: 0.65rem 1.3rem;
      background-color: var(--btn-bg);
      color: white;
      border-radius: 6px;
      text-decoration: none;
      font-weight: 600;
      font-size: 0.95rem;
      transition: background-color 0.3s ease;
      user-select: none;
    }
    .download-btn:hover {
      background-color: var(--btn-hover-bg);
      color: var(--primary-color);
    }

    /* Form */
    form#contact-form {
      display: flex;
      flex-direction: column;
      gap: 0.9rem;
      max-width: 450px;
      margin-top: 1rem;
    }
    input[type="text"],
    input[type="email"],
    textarea {
      padding: 0.6rem;
      font-size: 1rem;
      border-radius: 6px;
      border: 2px solid var(--input-border);
      transition: border-color 0.3s ease;
      font-family: inherit;
    }
    input[type="text"]:focus,
    input[type="email"]:focus,
    textarea:focus {
      border-color: var(--input-focus);
      outline: none;
    }
    textarea {
      resize: vertical;
      min-height: 80px;
      font-family: inherit;
    }
    button.submit-btn {
      padding: 0.7rem 1rem;
      font-size: 1rem;
      font-weight: 700;
      background-color: var(--btn-bg);
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      user-select: none;
      transition: background-color 0.3s ease;
      align-self: flex-start;
      min-width: 100px;
    }
    button.submit-btn:hover,
    button.submit-btn:focus {
      background-color: var(--btn-hover-bg);
      color: var(--primary-color);
      outline: none;
    }
    .form-message {
      margin-top: 0.5rem;
      font-weight: 600;
    }
    .form-message.success {
      color: #2e7d32;
    }
    .form-message.error {
      color: #c62828;
    }

    /* Map */
    #map {
      height: 350px;
      border-radius: 10px;
      box-shadow: 0 2px 6px rgb(0 0 0 / 0.1);
      transition: box-shadow 0.3s ease;
      margin-top: 0.7rem;
    }
    #map:hover {
      box-shadow: 0 3px 12px rgb(0 0 0 / 0.15);
    }

    /* Donation */
    .donation-section {
      text-align: center;
    }
    .donation-btn {
      display: inline-block;
      margin-top: 0.8rem;
      padding: 0.7rem 1.4rem;
      background-color: #0070ba;
      color: white;
      border: none;
      border-radius: 6px;
      font-weight: 700;
      font-size: 1rem;
      cursor: pointer;
      text-decoration: none;
      user-select: none;
      transition: background-color 0.3s ease;
    }
    .donation-btn:hover,
    .donation-btn:focus {
      background-color: #003087;
      outline: none;
    }

    /* Responsive */
    @media (max-width: 600px) {
      header {
        justify-content: center;
        gap: 0.8rem;
      }
      .animated-text {
        font-size: 1.6rem;
        margin-bottom: 1rem;
      }
      form#contact-form {
        max-width: 100%;
      }
      main {
        margin: 1rem 1rem 2rem;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>Silent Witness</h1>
    <div class="controls">
      <label for="lang-select" class="sr-only">Choisir la langue</label>
      <select id="lang-select" class="language-select" aria-label="Choisir la langue">
        <option value="fr" selected>Français</option>
        <option value="en">English</option>
        <option value="ar">العربية</option>
      </select>
      <button id="theme-toggle" aria-label="Basculer thème clair/sombre" title="Basculer thème clair/sombre">🌓</button>
    </div>
  </header>

  <main>
    <div class="animated-text" aria-live="polite" aria-atomic="true"></div>

    <section>
      <p id="wp-paragraph"></p>
      <a
        id="wp-btn"
        href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf"
        target="_blank"
        rel="noopener noreferrer"
        class="download-btn"
        >📘 Télécharger notre White Paper</a
      >
    </section>

    <section>
      <h2 id="stats-title">Statistiques clés</h2>
      <ul id="stats-list">
        <!-- remplissage JS -->
      </ul>
    </section>

    <section>
      <h2>Carte mondiale des suicides</h2>
      <div id="map" role="region" aria-label="Carte interactive des taux de suicide"></div>
    </section>

    <section>
      <h2>Étapes de détection IA</h2>
      <ol id="detection-steps">
        <!-- remplissage JS -->
      </ol>
    </section>

    <section class="donation-section">
      <h2>Contribuez à Silent Witness</h2>
      <p>Votre soutien est vital pour concrétiser ce projet et sauver des vies.</p>
      <div id="paypal-donation"></div>
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
          autocomplete="name"
        />
        <input
          id="input-email"
          type="email"
          name="email"
          placeholder="Votre email"
          required
          aria-required="true"
          autocomplete="email"
        />
        <textarea
          id="input-message"
          name="message"
          rows="4"
          placeholder="Votre message"
          required
          aria-required="true"
          autocomplete="off"
        ></textarea>
        <button type="submit" id="btn-send" class="submit-btn">Envoyer</button>
        <div id="form-message" role="alert" aria-live="assertive" class="form-message"></div>
      </form>
    </section>
  </main>

  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>

  <script>
    emailjs.init('_pR14KMi1syThzlmY');

    const translations = {
      fr: {
        title: "Vous n'êtes pas seul",
        whitepaper: "📘 Télécharger notre White Paper",
        paragraph:
          "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.",
        stats: [
          "Près de 800 000 personnes se suicident chaque année (OMS)",
          "1 suicide toutes les 40 secondes dans le monde",
          "Le suicide est la 2e cause de mortalité chez les 15-29 ans",
        ],
        steps: [
          "Analyse des mots clés dans les messages, requêtes IA ou recherches web",
          "Corrélation des données vocales, textuelles ou comportementales",
          "Évaluation automatique du niveau de détresse",
          "Classement de l’urgence (vert / orange / rouge)",
          "Déclenchement d'une alerte vers ONG, autorités ou hôpitaux selon le niveau",
        ],
        formSendSuccess: "Message envoyé avec succès ! Merci.",
        formSendError: "Erreur lors de l'envoi. Veuillez réessayer.",
        formSending: "Envoi en cours...",
        sendBtnText: "Envoyer",
      },
      en: {
        title: "You're not alone",
        whitepaper: "📘 Download our White Paper",
        paragraph:
          "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable.",
        stats: [
          "Nearly 800,000 people die by suicide each year (WHO)",
          "1 suicide every 40 seconds worldwide",
          "Suicide is the 2nd leading cause of death among 15-29 year olds",
        ],
        steps: [
          "Analyze keywords in messages, AI queries or web searches",
          "Correlate vocal, textual or behavioral data",
          "Automatically evaluate distress level",
          "Rank urgency (green / orange / red)",
          "Trigger alert to NGOs, authorities or hospitals based on level",
        ],
        formSendSuccess: "Message sent successfully! Thank you.",
        formSendError: "Sending failed. Please try again.",
        formSending: "Sending...",
        sendBtnText: "Send",
      },
      ar: {
        title: "لست وحدك",
        whitepaper: "📘 تحميل الورقة البيضاء",
        paragraph:
          "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر.",
        stats: [
          "يقع حوالي 800,000 شخص في حالات انتحار سنويًا (منظمة الصحة العالمية)",
          "انتحار واحد كل 40 ثانية في جميع أنحاء العالم",
          "الانتحار هو السبب الثاني للوفاة بين سن 15-29",
        ],
        steps: [
          "تحليل الكلمات المفتاحية في الرسائل أو استفسارات الذكاء الاصطناعي أو عمليات البحث على الويب",
          "ربط البيانات الصوتية والنصية والسلوكية",
          "التقييم التلقائي لمستوى الضيق النفسي",
          "تصنيف مستوى الطوارئ (أخضر / برتقالي / أحمر)",
          "إطلاق التنبيه إلى المنظمات غير الحكومية أو السلطات أو المستشفيات حسب المستوى",
        ],
        formSendSuccess: "تم إرسال الرسالة بنجاح! شكرًا لك.",
        formSendError: "حدث خطأ أثناء الإرسال. الرجاء المحاولة مرة أخرى.",
        formSending: "جارٍ الإرسال...",
        sendBtnText: "إرسال",
      },
    };

    let currentLang = "fr";

    function updateLanguage(lang) {
      const trans = translations[lang];
      document.querySelector(".animated-text").textContent = trans.title;
      document.getElementById("wp-paragraph").textContent = trans.paragraph;
      const wpBtn = document.getElementById("wp-btn");
      wpBtn.textContent = trans.whitepaper;

      // Statistiques
      const statsList = document.getElementById("stats-list");
      statsList.innerHTML = "";
      trans.stats.forEach((item) => {
        const li = document.createElement("li");
        li.textContent = item;
        statsList.appendChild(li);
      });

      // Étapes détection IA
      const stepsList = document.getElementById("detection-steps");
      stepsList.innerHTML = "";
      trans.steps.forEach((step) => {
        const li = document.createElement("li");
        li.textContent = step;
        stepsList.appendChild(li);
      });

      // Bouton formulaire
      const btnSend = document.getElementById("btn-send");
      btnSend.textContent = trans.sendBtnText;

      // Message formulaire reset
      formMessage.textContent = "";
      formMessage.className = "form-message";

      currentLang = lang;
    }

    function toggleTheme() {
      document.body.classList.toggle("dark-theme");
    }

    // EmailJS form handling
    const form = document.getElementById("contact-form");
    const formMessage = document.getElementById("form-message");

    form.addEventListener("submit", (e) => {
      e.preventDefault();
      formMessage.textContent = translations[currentLang].formSending;
      formMessage.className = "form-message";
      document.getElementById("btn-send").disabled = true;

      emailjs
        .sendForm("service_za2pm5i", "template_mt5ycpk", form)
        .then(() => {
          formMessage.textContent = translations[currentLang].formSendSuccess;
          formMessage.className = "form-message success";
          form.reset();
          document.getElementById("btn-send").disabled = false;
        })
        .catch(() => {
          formMessage.textContent = translations[currentLang].formSendError;
          formMessage.className = "form-message error";
          document.getElementById("btn-send").disabled = false;
        });
    });

    // Leaflet carte interactive
    function initMap() {
      const map = L.map("map", {
        center: [20, 0],
        zoom: 2,
        minZoom: 2,
        maxZoom: 6,
        scrollWheelZoom: false,
      });

      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution:
          '&copy; <a href="https://www.openstreetmap.org/copyright" target="_blank" rel="noopener noreferrer">OpenStreetMap</a> contributors',
      }).addTo(map);

      const suicideData = [
        { country: "France", coords: [46.2276, 2.2137], rate: 12.1 },
        { country: "USA", coords: [37.0902, -95.7129], rate: 14.5 },
        { country: "Brazil", coords: [-14.235, -51.9253], rate: 6.2 },
        { country: "Japan", coords: [36.2048, 138.2529], rate: 18.5 },
        { country: "India", coords: [20.5937, 78.9629], rate: 16.3 },
        { country: "South Africa", coords: [-30.5595, 22.9375], rate: 11.5 },
        { country: "Australia", coords: [-25.2744, 133.7751], rate: 12.9 },
        { country: "Russia", coords: [61.524, 105.3188], rate: 26.5 },
      ];

      suicideData.forEach(({ country, coords, rate }) => {
        let color = "#3cba54"; // vert
        if (rate > 20) color = "#db3236"; // rouge
        else if (rate > 15) color = "#f4c20d"; // orange

        const radius = rate * 8000;

        L.circle(coords, {
          color,
          fillColor: color,
          fillOpacity: 0.5,
          radius,
        })
          .addTo(map)
          .bindPopup(`<strong>${country}</strong><br>Taux de suicide: ${rate} / 100k habitants`);
      });
    }

    // PayPal Donation button injecté dans #paypal-donation
    function loadPaypalButton() {
      if (!window.paypal) return;
      paypal
        .Buttons({
          style: {
            shape: "rect",
            color: "blue",
            layout: "horizontal",
            label: "donate",
          },
          createOrder: function (data, actions) {
            return actions.order.create({
              purchase_units: [
                {
                  amount: {
                    value: "5.00", // montant par défaut, modifiable par l'utilisateur
                  },
                },
              ],
            });
          },
          onApprove: function (data, actions) {
            return actions.order.capture().then(function () {
              alert("Merci pour votre don !");
            });
          },
        })
        .render("#paypal-donation");
    }

    // Au chargement
    window.addEventListener("DOMContentLoaded", () => {
      updateLanguage(currentLang);
      initMap();
      loadPaypalButton();

      document
        .getElementById("lang-select")
        .addEventListener("change", (e) => updateLanguage(e.target.value));

      document.getElementById("theme-toggle").addEventListener("click", toggleTheme);
    });
  </script>

  <!-- PayPal SDK -->
  <script
    src="https://www.paypal.com/sdk/js?client-id=BAAwNQmuQNtmwbB198XpnMFgJqBHvKNcvg138E9ddcIrNxHGCrGT2tvdVOyLaJTqde8dM-9e9ZglZUXS9A&currency=USD"
    data-sdk-integration-source="button-factory"
  ></script>
</body>
</html>

