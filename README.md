<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Silent Witness - Vous n'êtes pas seul</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins&family=Cairo&display=swap');
  :root {
    --clr-bg-light: #f9fafb;
    --clr-bg-dark: #1c1c1c;
    --clr-text-light: #1c5980;
    --clr-text-dark: #f0f0f0;
    --clr-primary: #1c5980;
    --clr-primary-light: #8fc1a1;
    --clr-success: #3cba54;
    --clr-warning: #f4c20d;
    --clr-danger: #db3236;
    --transition: 0.3s ease-in-out;
  }
  body {
    margin: 0; padding: 0;
    font-family: 'Poppins', sans-serif;
    background: var(--clr-bg-light);
    color: var(--clr-text-light);
    line-height: 1.5;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  body.dark-theme {
    background: var(--clr-bg-dark);
    color: var(--clr-text-dark);
  }
  header {
    background: var(--clr-primary);
    color: #fff;
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
  }
  header h1 {
    margin: 0;
    font-family: 'Cairo', sans-serif;
    font-weight: 700;
    font-size: 1.8rem;
  }
  .controls {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  select#lang-select {
    padding: 0.3rem 0.6rem;
    border-radius: 6px;
    border: none;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
  }
  button#theme-toggle {
    background: transparent;
    border: none;
    font-size: 1.4rem;
    cursor: pointer;
    color: #fff;
    user-select: none;
  }

  main {
    flex-grow: 1;
    max-width: 1200px;
    margin: 2rem auto;
    padding: 0 1rem;
    width: 100%;
  }
  .animated-text {
    text-align: center;
    font-weight: 700;
    font-size: 2.5rem;
    margin-bottom: 1rem;
    animation: pulse 2.5s infinite;
  }
  @keyframes pulse {
    0%, 100% {opacity: 1; transform: scale(1);}
    50% {opacity: 0.6; transform: scale(1.05);}
  }

  section {
    margin-bottom: 3rem;
  }
  h2 {
    font-family: 'Cairo', sans-serif;
    font-weight: 700;
    color: var(--clr-primary);
    margin-bottom: 1rem;
    font-size: 1.8rem;
  }

  /* White Paper */
  .whitepaper {
    background: var(--clr-primary-light);
    padding: 1rem 1.5rem;
    border-radius: 8px;
    color: var(--clr-primary);
    font-weight: 600;
    display: inline-block;
    cursor: pointer;
    text-decoration: none;
    user-select: none;
    transition: background var(--transition), color var(--transition);
  }
  .whitepaper:hover, .whitepaper:focus {
    background: var(--clr-primary);
    color: #fff;
    outline: none;
  }

  /* Stats */
  ul.stats-list {
    list-style: inside disc;
    font-size: 1.1rem;
    max-width: 700px;
    margin: 0 auto;
  }

  /* Compteur suicides */
  #suicide-counter {
    text-align: center;
    font-size: 1.4rem;
    font-weight: 700;
    margin: 1rem 0 0.5rem;
    color: var(--clr-danger);
    font-family: 'Cairo', sans-serif;
  }

  /* Timeline étapes IA */
  ol.timeline {
    counter-reset: step-counter;
    max-width: 750px;
    margin: 0 auto;
    padding-left: 1.5rem;
  }
  ol.timeline li {
    position: relative;
    padding-left: 2.8rem;
    margin-bottom: 1.5rem;
    font-size: 1.1rem;
    line-height: 1.3;
  }
  ol.timeline li::before {
    content: counter(step-counter);
    counter-increment: step-counter;
    position: absolute;
    left: 0;
    top: 0;
    background: var(--clr-primary);
    color: white;
    font-weight: 700;
    width: 1.8rem;
    height: 1.8rem;
    border-radius: 50%;
    text-align: center;
    line-height: 1.8rem;
    user-select: none;
  }
  ol.timeline li:nth-child(4)::before {
    background: var(--clr-warning);
  }
  ol.timeline li:nth-child(5)::before {
    background: var(--clr-danger);
  }

  /* Carte interactive */
  #map {
    width: 100%;
    height: 400px;
    max-width: 900px;
    margin: 1.5rem auto;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(28, 89, 128, 0.3);
  }

  /* Formulaire */
  form#contact-form {
    max-width: 600px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  form#contact-form input,
  form#contact-form textarea {
    padding: 0.8rem;
    border-radius: 6px;
    border: 1.5px solid #ccc;
    font-size: 1rem;
    font-family: 'Poppins', sans-serif;
    resize: vertical;
  }
  form#contact-form input:focus,
  form#contact-form textarea:focus {
    outline: none;
    border-color: var(--clr-primary);
    box-shadow: 0 0 4px var(--clr-primary);
  }
  form#contact-form button {
    background: var(--clr-primary);
    color: white;
    border: none;
    padding: 0.9rem 1rem;
    font-size: 1.1rem;
    font-weight: 700;
    border-radius: 6px;
    cursor: pointer;
    transition: background var(--transition);
  }
  form#contact-form button:disabled {
    background: #a0b8c8;
    cursor: not-allowed;
  }
  form#contact-form button:hover:not(:disabled),
  form#contact-form button:focus:not(:disabled) {
    background: var(--clr-primary-light);
    outline: none;
  }

  /* Message succès/erreur */
  #form-message {
    text-align: center;
    font-weight: 600;
    font-size: 1rem;
    min-height: 1.4rem;
  }
  #form-message.success {
    color: var(--clr-success);
  }
  #form-message.error {
    color: var(--clr-danger);
  }

  /* Donation PayPal */
  #paypal-donation {
    max-width: 300px;
    margin: 0 auto;
    text-align: center;
  }

  /* Retour en haut */
  #back-to-top {
    position: fixed;
    bottom: 1.5rem;
    right: 1.5rem;
    background: var(--clr-primary);
    color: #fff;
    border-radius: 50%;
    width: 42px;
    height: 42px;
    font-size: 1.8rem;
    cursor: pointer;
    display: none;
    align-items: center;
    justify-content: center;
    box-shadow: 0 0 6px rgba(28, 89, 128, 0.6);
    transition: background var(--transition);
    user-select: none;
    z-index: 9999;
  }
  #back-to-top:hover {
    background: var(--clr-primary-light);
  }

  /* FAQ */
  .faq {
    max-width: 800px;
    margin: 0 auto;
  }
  .faq dt {
    font-weight: 700;
    margin-top: 1rem;
    cursor: pointer;
    color: var(--clr-primary);
  }
  .faq dd {
    margin: 0.25rem 0 1rem 1rem;
    display: none;
    font-size: 1rem;
  }
  .faq dt.active + dd {
    display: block;
  }

  /* Responsive */
  @media (max-width: 720px) {
    header {
      justify-content: center;
      gap: 1rem;
      text-align: center;
    }
    header h1 {
      font-size: 1.5rem;
    }
    .animated-text {
      font-size: 1.8rem;
    }
    #map {
      height: 300px;
    }
  }
</style>
<!-- Leaflet CSS -->
<link
  rel="stylesheet"
  href="https://unpkg.com/leaflet@1.9.3/dist/leaflet.css"
  integrity="sha256-sA+Q41H+I+ftMy8J50i+JqYt0P8OYnd2V8taT4U/7C4="
  crossorigin=""
/>
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
    <button id="theme-toggle" aria-label="Basculer thème clair/sombre" title="Basculer thème clair/sombre">🌓</button>
  </div>
</header>
<main>
  <div class="animated-text" id="animated-text">Vous n'êtes pas seul</div>

  <section aria-labelledby="whitepaper-title">
    <h2 id="whitepaper-title">Livre blanc Silent Witness</h2>
    <p id="wp-paragraph">
      Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.
    </p>
    <a
      href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf"
      target="_blank"
      rel="noopener"
      class="whitepaper"
      id="wp-btn"
      >📘 Télécharger le White Paper</a
    >
  </section>

  <section aria-labelledby="stats-title">
    <h2 id="stats-title">Statistiques sur le suicide</h2>
    <ul class="stats-list" id="stats-list">
      <li>Près de 800 000 personnes se suicident chaque année (OMS)</li>
      <li>1 suicide toutes les 40 secondes dans le monde</li>
      <li>Le suicide est la 2e cause de mortalité chez les 15-29 ans</li>
    </ul>
    <div id="suicide-counter" aria-live="polite" aria-atomic="true">1 suicide toutes les 40 secondes</div>
  </section>

  <section aria-labelledby="detection-title">
    <h2 id="detection-title">Étapes de détection IA</h2>
    <ol class="timeline" id="timeline">
      <li>Analyse des mots clés dans les messages, requêtes IA ou recherches web</li>
      <li>Corrélation des données vocales, textuelles ou comportementales</li>
      <li>Évaluation automatique du niveau de détresse</li>
      <li>Classement de l’urgence (vert / orange / rouge)</li>
      <li>Déclenchement d'une alerte vers ONG, autorités ou hôpitaux selon le niveau</li>
    </ol>
  </section>

  <section aria-labelledby="map-title">
    <h2 id="map-title">Carte interactive mondiale des taux de suicide</h2>
    <div id="map" role="region" aria-label="Carte interactive des taux de suicide par pays"></div>
  </section>

  <section aria-labelledby="contact-title">
    <h2 id="contact-title">Contact</h2>
    <form id="contact-form" aria-describedby="form-message" novalidate>
      <input type="text" name="nom" placeholder="Votre nom" required aria-required="true" />
      <input type="email" name="email" placeholder="Votre email" required aria-required="true" />
      <textarea name="message" placeholder="Votre message" rows="4" required aria-required="true"></textarea>
      <button type="submit" id="submit-btn">Envoyer</button>
    </form>
    <div id="form-message" role="alert" aria-live="assertive"></div>
  </section>

  <section aria-labelledby="donation-title" style="text-align:center;">
    <h2 id="donation-title">Soutenez Silent Witness</h2>
    <p>Votre don contribue à concrétiser ce projet de prévention et protection.</p>
    <div id="paypal-donation"></div>
  </section>

  <section aria-labelledby="faq-title" class="faq">
    <h2 id="faq-title">FAQ - Questions fréquentes</h2>
    <dl>
      <dt tabindex="0">Comment garantissez-vous la confidentialité des données ?</dt>
      <dd>Silent Witness utilise des protocoles stricts et ne partage aucune donnée sans consentement explicite.</dd>
      <dt tabindex="0">Comment fonctionne la détection ?</dt>
      <dd>Notre IA analyse des indicateurs clés dans les communications et comportements en temps réel pour évaluer la détresse.</dd>
      <dt tabindex="0">Puis-je rester anonyme ?</dt>
      <dd>Oui, l’utilisation peut être anonyme et les alertes sont traitées de manière confidentielle.</dd>
    </dl>
  </section>
</main>

<button id="back-to-top" aria-label="Retour en haut" title="Retour en haut">↑</button>

<!-- Leaflet JS -->
<script
  src="https://unpkg.com/leaflet@1.9.3/dist/leaflet.js"
  integrity="sha256-oC4PvAoMkruNqJtv5T3Y2T/f+v3GmrL0PslbkD5tpzE="
  crossorigin=""
></script>
<!-- EmailJS SDK -->
<script src="https://cdn.emailjs.com/dist/email.min.js"></script>
<!-- PayPal SDK -->
<script
  src="https://www.paypal.com/sdk/js?client-id=BAAwNQmuQNtmwbB198XpnMFgJqBHvKNcvg138E9ddcIrNxHGCrGT2tvdVOyLaJTqde8dM-9e9ZglZUXS9A&currency=USD"
  data-sdk-integration-source="button-factory"
></script>
<script>
  // Initialisation EmailJS
  emailjs.init('_pR14KMi1syThzlmY');

  // Traductions complètes
  const translations = {
    fr: {
      animatedText: "Vous n'êtes pas seul",
      whitepaper: "📘 Télécharger le White Paper",
      wpParagraph:
        "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.",
      stats: [
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
      contactPlaceholder: {
        nom: "Votre nom",
        email: "Votre email",
        message: "Votre message",
        button: "Envoyer",
      },
      donationTitle: "Soutenez Silent Witness",
      donationParagraph:
        "Votre don contribue à concrétiser ce projet de prévention et protection.",
      formSuccess: "Message envoyé avec succès, merci !",
      formError: "Erreur lors de l'envoi, veuillez réessayer.",
    },
    en: {
      animatedText: "You're not alone",
      whitepaper: "📘 Download our White Paper",
      wpParagraph:
        "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable.",
      stats: [
        "Nearly 800,000 people die by suicide each year (WHO)",
        "1 suicide every 40 seconds worldwide",
        "Suicide is the 2nd leading cause of death among 15-29 year olds",
      ],
      detectionTitle: "AI Detection Steps",
      detectionSteps: [
        "Analyze keywords in messages, AI queries, or web searches",
        "Correlate vocal, textual, or behavioral data",
        "Automatically evaluate distress level",
        "Urgency ranking (green / orange / red)",
        "Trigger alert to NGOs, authorities or hospitals depending on level",
      ],
      contactTitle: "Contact",
      contactPlaceholder: {
        nom: "Your name",
        email: "Your email",
        message: "Your message",
        button: "Send",
      },
      donationTitle: "Support Silent Witness",
      donationParagraph:
        "Your donation helps bring this prevention and protection project to life.",
      formSuccess: "Message sent successfully, thank you!",
      formError: "Error sending message, please try again.",
    },
    ar: {
      animatedText: "لست وحدك",
      whitepaper: "📘 تحميل الورقة البيضاء",
      wpParagraph:
        "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر.",
      stats: [
        "يُقدّر أن 800,000 شخص ينتحرون سنويًا (منظمة الصحة العالمية)",
        "انتحار واحد كل 40 ثانية في العالم",
        "الانتحار هو السبب الثاني للوفاة بين 15-29 سنة",
      ],
      detectionTitle: "خطوات الكشف بالذكاء الاصطناعي",
      detectionSteps: [
        "تحليل الكلمات المفتاحية في الرسائل أو طلبات الذكاء الاصطناعي أو البحث على الإنترنت",
        "ربط البيانات الصوتية والنصية أو السلوكية",
        "التقييم التلقائي لمستوى الضيق",
        "تصنيف درجة الاستعجال (أخضر / برتقالي / أحمر)",
        "إطلاق تنبيه إلى المنظمات والسلطات والمستشفيات حسب المستوى",
      ],
      contactTitle: "اتصل بنا",
      contactPlaceholder: {
        nom: "اسمك",
        email: "بريدك الإلكتروني",
        message: "رسالتك",
        button: "إرسال",
      },
      donationTitle: "ادعم Silent Witness",
      donationParagraph:
        "تبرعك يساعد على إنجاح هذا المشروع للوقاية والحماية.",
      formSuccess: "تم إرسال الرسالة بنجاح، شكرًا لك!",
      formError: "حدث خطأ أثناء الإرسال، الرجاء المحاولة مرة أخرى.",
    },
  };

  // Elements references
  const langSelect = document.getElementById("lang-select");
  const animatedText = document.getElementById("animated-text");
  const wpBtn = document.getElementById("wp-btn");
  const wpParagraph = document.getElementById("wp-paragraph");
  const statsList = document.getElementById("stats-list");
  const timeline = document.getElementById("timeline");
  const contactForm = document.getElementById("contact-form");
  const formMessage = document.getElementById("form-message");
  const submitBtn = document.getElementById("submit-btn");
  const donationTitle = document.getElementById("donation-title");
  const donationParagraph = document.querySelector("#paypal-donation").previousElementSibling;

  function updateContent(lang) {
    const t = translations[lang];

    animatedText.textContent = t.animatedText;
    wpBtn.textContent = t.whitepaper;
    wpParagraph.textContent = t.wpParagraph;

    // Stats
    statsList.innerHTML = "";
    t.stats.forEach((item) => {
      const li = document.createElement("li");
      li.textContent = item;
      statsList.appendChild(li);
    });

    // Detection steps
    timeline.innerHTML = "";
    t.detectionSteps.forEach((step) => {
      const li = document.createElement("li");
      li.textContent = step;
      timeline.appendChild(li);
    });

    // Contact placeholders
    contactForm.nom.placeholder = t.contactPlaceholder.nom;
    contactForm.email.placeholder = t.contactPlaceholder.email;
    contactForm.message.placeholder = t.contactPlaceholder.message;
    submitBtn.textContent = t.contactPlaceholder.button;

    // Donation text
    donationTitle.textContent = t.donationTitle;
    donationParagraph.textContent = t.donationParagraph;

    // Reset form messages
    formMessage.textContent = "";
    formMessage.className = "";
  }

  // Handle language change
  langSelect.addEventListener("change", (e) => {
    updateContent(e.target.value);
    if (e.target.value === "ar") {
      document.body.dir = "rtl";
      document.body.style.fontFamily = "'Cairo', sans-serif";
    } else {
      document.body.dir = "ltr";
      document.body.style.fontFamily = "'Poppins', sans-serif";
    }
  });

  // Theme toggle
  const themeToggle = document.getElementById("theme-toggle");
  function applyTheme(dark) {
    if (dark) document.body.classList.add("dark-theme");
    else document.body.classList.remove("dark-theme");
  }
  function getPrefersDark() {
    return window.matchMedia && window.matchMedia("(prefers-color-scheme: dark)").matches;
  }
  // Initial theme based on preference or hour
  function initTheme() {
    const hour = new Date().getHours();
    if (getPrefersDark() || hour >= 19 || hour < 7) {
      applyTheme(true);
    } else {
      applyTheme(false);
    }
  }
  themeToggle.addEventListener("click", () => {
    const isDark = document.body.classList.toggle("dark-theme");
    localStorage.setItem("theme", isDark ? "dark" : "light");
  });
  window.onload = () => {
    const savedTheme = localStorage.getItem("theme");
    if (savedTheme) applyTheme(savedTheme === "dark");
    else initTheme();
  };

  // EmailJS form handling
  contactForm.addEventListener("submit", (e) => {
    e.preventDefault();
    submitBtn.disabled = true;
    formMessage.textContent = "";
    formMessage.className = "";

    emailjs
      .sendForm("service_za2pm5i", "template_mt5ycpk", contactForm)
      .then(() => {
        formMessage.textContent = translations[langSelect.value].formSuccess;
        formMessage.classList.add("success");
        contactForm.reset();
      })
      .catch(() => {
        formMessage.textContent = translations[langSelect.value].formError;
        formMessage.classList.add("error");
      })
      .finally(() => {
        submitBtn.disabled = false;
      });
  });

  // Back to top button
  const backToTopBtn = document.getElementById("back-to-top");
  window.addEventListener("scroll", () => {
    if (window.scrollY > 300) backToTopBtn.style.display = "flex";
    else backToTopBtn.style.display = "none";
  });
  backToTopBtn.addEventListener("click", () => {
    window.scrollTo({ top: 0, behavior: "smooth" });
  });

  // Compteur animé (simulateur)
  const suicideCounter = document.getElementById("suicide-counter");
  let count = 0;
  const interval = 40 * 1000; // 40 sec
  function incrementCounter() {
    count++;
    suicideCounter.textContent = `${count} suicide${count > 1 ? "s" : ""} depuis que vous êtes ici.`;
  }
  setInterval(incrementCounter, interval);

  // Leaflet carte interactive avec données
  const map = L.map("map").setView([20, 0], 2);

  L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
    maxZoom: 6,
    attribution: '© OpenStreetMap contributors',
  }).addTo(map);

  // Données simplifiées taux suicide par 100k habitants (exemple)
  const suicideRates = {
    FR: 15.1,
    US: 14.5,
    MA: 11.2,
    IN: 16.5,
    CN: 8.5,
    RU: 26.5,
    BR: 6.2,
    ZA: 12.8,
  };

  // Polygones GeoJSON simplifié pays clés (exemple)
  // On utilise Leaflet's CircleMarkers instead for simplicity
  Object.entries(suicideRates).forEach(([countryCode, rate]) => {
    // Coords approximatives (lat, lng) pour quelques pays (à ajuster)
    const coords = {
      FR: [46.6, 2.4],
      US: [39.8, -98.6],
      MA: [31.6, -7.9],
      IN: [21.0, 78.0],
      CN: [35.9, 104.2],
      RU: [61.5, 105.3],
      BR: [-14.2, -51.9],
      ZA: [-30.5, 22.9],
    }[countryCode];
    if (!coords) return;
    const color =
      rate < 10 ? "#3cba54" : rate < 15 ? "#f4c20d" : "#db3236";

    L.circleMarker(coords, {
      radius: 15,
      fillColor: color,
      color: "#222",
      weight: 1,
      opacity: 1,
      fillOpacity: 0.7,
    })
      .addTo(map)
      .bindPopup(
        `<b>${countryCode}</b><br>Taux de suicide: ${rate} / 100k habitants`
      );
  });

  // FAQ accordion
  document.querySelectorAll(".faq dt").forEach((dt) => {
    dt.addEventListener("click", () => {
      dt.classList.toggle("active");
    });
    dt.addEventListener("keydown", (e) => {
      if (e.key === "Enter" || e.key === " ") {
        e.preventDefault();
        dt.classList.toggle("active");
      }
    });
  });

  // Initial update
  updateContent(langSelect.value);
</script>

<!-- PayPal Buttons -->
<script>
  paypal.Buttons({
    style: {
      shape: 'pill',
      color: 'blue',
      layout: 'vertical',
      label: 'donate',
    },
    createOrder: function(data, actions) {
      return actions.order.create({
        purchase_units: [{
          amount: {
            value: '5.00' // montant par défaut en USD
          }
        }]
      });
    },
    onApprove: function(data, actions) {
      return actions.order.capture().then(function(details) {
        alert('Merci pour votre don, ' + details.payer.name.given_name + '!');
      });
    }
  }).render('#paypal-donation');
</script>
</body>
</html>

