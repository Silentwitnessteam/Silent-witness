<html lang="fr" dir="ltr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Silent Witness</title>

<!-- Poppins font -->
<link href="https://fonts.googleapis.com/css2?family=Poppins&family=Cairo&display=swap" rel="stylesheet" />

<!-- Leaflet CSS -->
<link
  rel="stylesheet"
  href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
  integrity="sha256-sA+1PnMd0EOhWqIM6AP6GIh1q5r4n0bV0v00Pe5MQ1s="
  crossorigin=""
/>

<style>
  :root {
    --color-primary: #1c5980;
    --color-secondary: #8fc1a1;
    --bg-light: #ffffff;
    --text-light: #1c5980;
    --bg-dark: #1c1c1c;
    --text-dark: #f0f0f0;
  }
  body {
    margin: 0; 
    font-family: 'Poppins', sans-serif;
    background-color: var(--bg-light);
    color: var(--text-light);
    transition: background-color 0.3s, color 0.3s;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  body.dark-theme {
    background-color: var(--bg-dark);
    color: var(--text-dark);
  }
  header {
    background: var(--color-primary);
    color: white;
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
  }
  header h1 {
    margin: 0;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  header h1 img {
    height: 40px;
    width: auto;
    border-radius: 6px;
  }
  .controls {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  select.language-select {
    padding: 0.4rem 0.6rem;
    font-family: 'Poppins', sans-serif;
    font-weight: 600;
    border-radius: 6px;
    border: none;
    cursor: pointer;
  }
  button#theme-toggle {
    background: var(--color-secondary);
    border: none;
    border-radius: 6px;
    padding: 0.5rem 0.8rem;
    cursor: pointer;
    font-size: 1.3rem;
    transition: background-color 0.3s;
  }
  button#theme-toggle:hover {
    background: #6aa173;
  }
  main {
    flex: 1;
    padding: 2rem;
    max-width: 1100px;
    margin: auto;
    width: 100%;
  }
  .animated-text {
    font-size: 2.5rem;
    font-weight: 700;
    text-align: center;
    margin-bottom: 2rem;
    animation: pulseText 2.5s ease-in-out infinite;
  }
  /* Pulse animation */
  @keyframes pulseText {
    0%,100% {opacity: 1; transform: scale(1);}
    50% {opacity: 0.6; transform: scale(1.05);}
  }
  /* Multilingual uniformity */
  body[lang="ar"] {
    font-family: 'Cairo', sans-serif;
    direction: rtl;
  }
  body[lang="ar"] .animated-text {
    font-size: 2.5rem !important;
    line-height: 1.2;
  }
  /* White Paper Section */
  .whitepaper-section {
    text-align: center;
    margin-bottom: 3rem;
  }
  .whitepaper-section p {
    font-size: 1.2rem;
    margin-bottom: 1rem;
  }
  .download-btn {
    display: inline-block;
    background: var(--color-primary);
    color: white;
    padding: 0.8rem 1.5rem;
    border-radius: 8px;
    text-decoration: none;
    font-weight: 700;
    transition: background-color 0.3s;
  }
  .download-btn:hover {
    background: var(--color-secondary);
    color: var(--color-primary);
  }
  /* Carte Section */
  #map {
    height: 450px;
    border-radius: 8px;
    margin-bottom: 1rem;
    box-shadow: 0 0 12px rgba(0,0,0,0.15);
  }
  /* Filters */
  .filter-buttons {
    text-align: center;
    margin-bottom: 1.5rem;
  }
  .filter-buttons button {
    margin: 0 0.5rem;
    padding: 0.5rem 1rem;
    border: 2px solid var(--color-primary);
    background: white;
    color: var(--color-primary);
    font-weight: 700;
    border-radius: 6px;
    cursor: pointer;
    transition: background-color 0.3s,color 0.3s;
  }
  .filter-buttons button.active, .filter-buttons button:hover {
    background-color: var(--color-primary);
    color: white;
  }
  /* Stats section */
  .stats-section {
    background: #f2f7f1;
    padding: 1.5rem 2rem;
    border-radius: 8px;
    margin-bottom: 3rem;
    color: #1c5980;
  }
  body.dark-theme .stats-section {
    background: #283537;
    color: #a7d1b6;
  }
  .stats-section ul {
    list-style: inside disc;
    font-size: 1.15rem;
    line-height: 1.5;
  }
  /* Live stats */
  .live-stats {
    background: var(--color-secondary);
    color: var(--color-primary);
    padding: 1rem 1.5rem;
    border-radius: 8px;
    margin-bottom: 3rem;
    font-weight: 700;
    text-align: center;
    font-size: 1.15rem;
  }
  /* Steps detection */
  .steps-section ol {
    font-size: 1.1rem;
    padding-left: 1.4rem;
    line-height: 1.5;
  }
  /* Contact form */
  section.contact-section form {
    max-width: 500px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  section.contact-section input,
  section.contact-section textarea {
    padding: 0.75rem;
    border-radius: 6px;
    border: 1px solid #ccc;
    font-size: 1rem;
    font-family: 'Poppins', sans-serif;
  }
  section.contact-section textarea {
    resize: vertical;
    min-height: 100px;
  }
  section.contact-section button {
    background: var(--color-primary);
    color: white;
    border: none;
    padding: 0.75rem;
    font-weight: 700;
    border-radius: 6px;
    cursor: pointer;
    font-size: 1.1rem;
    transition: background-color 0.3s;
  }
  section.contact-section button:hover {
    background: var(--color-secondary);
    color: var(--color-primary);
  }
  /* Paypal button container */
  #paypal-button-container {
    max-width: 320px;
    margin: 2rem auto 3rem;
  }
  /* Responsive */
  @media (max-width: 700px) {
    header {
      justify-content: center;
      gap: 1rem;
    }
    header h1 {
      font-size: 1.5rem;
    }
    .animated-text {
      font-size: 1.8rem;
    }
    #map {
      height: 320px;
    }
    .stats-section ul {
      font-size: 1rem;
    }
  }
</style>
</head>
<body lang="fr" dir="ltr">
<header>
  <h1>
    <img src="https://cdn-icons-png.flaticon.com/512/1085/1085679.png" alt="IA et humain main dans la main" />
    Silent Witness
  </h1>
  <div class="controls">
    <select id="lang-select" class="language-select" aria-label="Choisir la langue">
      <option value="fr">🇫🇷 Français</option>
      <option value="en">🇬🇧 English</option>
      <option value="ar">🇸🇦 العربية</option>
    </select>
    <button id="theme-toggle" aria-label="Basculer thème clair/sombre">🌓</button>
  </div>
</header>

<main>
  <div class="animated-text" id="animated-text">Vous n'êtes pas seul</div>

  <section class="whitepaper-section" aria-label="Section livre blanc">
    <p id="wp-paragraph">Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.</p>
    <a id="wp-btn" href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf" target="_blank" class="download-btn" rel="noopener noreferrer" download>
      📘 Télécharger notre White Paper
    </a>
  </section>

  <section aria-label="Carte mondiale des suicides" class="map-section">
    <div class="filter-buttons" role="group" aria-label="Filtres carte interactive">
      <button class="active" data-filter="all" type="button">Tous</button>
      <button data-filter="men" type="button">Hommes</button>
      <button data-filter="women" type="button">Femmes</button>
      <button data-filter="youth" type="button">Jeunes</button>
      <button data-filter="domestic" type="button">Violences conjugales</button>
    </div>
    <div id="map" tabindex="0" aria-label="Carte interactive des taux de suicide"></div>
  </section>

  <section class="live-stats" aria-live="polite" aria-atomic="true" aria-label="Statistiques en temps réel">
    🌍 Une tentative de suicide chaque <strong>20 secondes</strong> dans le monde.<br />
    🧠 60% des victimes n'ont jamais parlé à personne.<br />
    💔 1 femme sur 3 subit des violences en silence.
  </section>

  <section aria-label="Statistiques clés" class="stats-section">
    <h2>Statistiques clés sur le suicide</h2>
    <ul>
      <li>Près de 800 000 personnes se suicident chaque année (OMS)</li>
      <li>1 suicide toutes les 40 secondes dans le monde</li>
      <li>Le suicide est la 2e cause de mortalité chez les 15-29 ans</li>
    </ul>
  </section>

  <section aria-label="Étapes de détection IA" class="steps-section">
    <h2>Étapes de détection IA</h2>
    <ol>
      <li>Analyse des mots clés dans les messages, requêtes IA ou recherches web</li>
      <li>Corrélation des données vocales, textuelles ou comportementales</li>
      <li>Évaluation automatique du niveau de détresse</li>
      <li>Classement de l’urgence (vert / orange / rouge)</li>
      <li>Déclenchement d'une alerte vers ONG, autorités ou hôpitaux selon le niveau</li>
    </ol>
  </section>

  <section aria-label="Formulaire de contact" class="contact-section">
    <h2>Contact</h2>
    <form id="contact-form" aria-label="Formulaire de contact">
      <input type="text" name="nom" placeholder="Votre nom" required aria-required="true" />
      <input type="email" name="email" placeholder="Votre email" required aria-required="true" />
      <textarea name="message" rows="4" placeholder="Votre message" required aria-required="true"></textarea>
      <button type="submit">Envoyer</button>
    </form>
  </section>

  <section aria-label="Donation" id="donation-section" style="text-align:center;">
    <h2>Contribuez au projet Silent Witness</h2>
    <div id="paypal-button-container" aria-label="Bouton de donation PayPal"></div>
  </section>
</main>

<!-- Leaflet JS -->
<script
  src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"
  integrity="sha256-o9N1j6gxIs0g3FHi9U/4d0wZcPHEf1DcZG7C1cURyMY="
  crossorigin=""
></script>

<!-- EmailJS -->
<script src="https://cdn.emailjs.com/dist/email.min.js"></script>

<!-- PayPal SDK -->
<script src="https://www.paypal.com/sdk/js?client-id=BAAwNQmuQNtmwbB198XpnMFgJqBHvKNcvg138E9ddcIrNxHGCrGT2tvdVOyLaJTqde8dM-9e9ZglZUXS9A&currency=USD"></script>

<script>
  // Init EmailJS
  emailjs.init('_pR14KMi1syThzlmY');

  // Multilingue texte
  const translations = {
    fr: {
      title: "Vous n'êtes pas seul",
      whitepaper: "📘 Télécharger notre White Paper",
      paragraph: "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.",
      donation: "Contribuez au projet Silent Witness",
      contactSend: "Envoyer",
      filters: {
        all: "Tous",
        men: "Hommes",
        women: "Femmes",
        youth: "Jeunes",
        domestic: "Violences conjugales"
      }
    },
    en: {
      title: "You're not alone",
      whitepaper: "📘 Download our White Paper",
      paragraph: "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable.",
      donation: "Support the Silent Witness project",
      contactSend: "Send",
      filters: {
        all: "All",
        men: "Men",
        women: "Women",
        youth: "Youth",
        domestic: "Domestic violence"
      }
    },
    ar: {
      title: "لست وحدك",
      whitepaper: "📘 تحميل الورقة البيضاء",
      paragraph: "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر.",
      donation: "ساهم في مشروع Silent Witness",
      contactSend: "إرسال",
      filters: {
        all: "الكل",
        men: "رجال",
        women: "نساء",
        youth: "الشباب",
        domestic: "العنف الأسري"
      }
    }
  };

  // Set initial lang/fr
  let currentLang = "fr";

  // Elements to update
  const animatedText = document.getElementById("animated-text");
  const wpParagraph = document.getElementById("wp-paragraph");
  const wpBtn = document.getElementById("wp-btn");
  const donationSection = document.getElementById("donation-section");
  const langSelect = document.getElementById("lang-select");
  const contactForm = document.getElementById("contact-form");
  const paypalContainer = document.getElementById("paypal-button-container");
  const filterButtons = document.querySelectorAll(".filter-buttons button");

  // Update texts on language change
  function updateTexts(lang) {
    currentLang = lang;
    document.documentElement.lang = lang;
    document.body.dir = lang === "ar" ? "rtl" : "ltr";

    animatedText.textContent = translations[lang].title;
    wpParagraph.textContent = translations[lang].paragraph;
    wpBtn.textContent = translations[lang].whitepaper;
    donationSection.querySelector("h2").textContent = translations[lang].donation;
    contactForm.querySelector("button[type=submit]").textContent = translations[lang].contactSend;

    // Update filter buttons text
    filterButtons.forEach(btn => {
      const key = btn.getAttribute("data-filter");
      btn.textContent = translations[lang].filters[key];
    });
  }

  langSelect.addEventListener("change", (e) => {
    updateTexts(e.target.value);
  });

  // Theme toggle
  const themeToggle = document.getElementById("theme-toggle");
  themeToggle.addEventListener("click", () => {
    document.body.classList.toggle("dark-theme");
  });

  // EmailJS form send
  contactForm.addEventListener("submit", (e) => {
    e.preventDefault();
    emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', e.target)
      .then(() => {
        alert(currentLang === "fr" ? "Message envoyé !" : currentLang === "en" ? "Message sent!" : "تم إرسال الرسالة!");
        contactForm.reset();
      })
      .catch(() => {
        alert(currentLang === "fr" ? "Erreur lors de l'envoi." : currentLang === "en" ? "Failed to send message." : "فشل في إرسال الرسالة.");
      });
  });

  // Données suicide (exemple réel simplifié, OMS + OurWorldInData + ajusté)
  const suicideData = {
    all: [
      { continent: "Africa", rate: 7.5 },
      { continent: "Asia", rate: 9.4 },
      { continent: "Europe", rate: 11.2 },
      { continent: "North America", rate: 13.1 },
      { continent: "Oceania", rate: 14.0 },
      { continent: "South America", rate: 6.3 },
    ],
    men: [
      { continent: "Africa", rate: 11.2 },
      { continent: "Asia", rate: 14.5 },
      { continent: "Europe", rate: 15.8 },
      { continent: "North America", rate: 18.4 },
      { continent: "Oceania", rate: 20.1 },
      { continent: "South America", rate: 8.7 },
    ],
    women: [
      { continent: "Africa", rate: 4.1 },
      { continent: "Asia", rate: 4.3 },
      { continent: "Europe", rate: 6.5 },
      { continent: "North America", rate: 7.1 },
      { continent: "Oceania", rate: 7.4 },
      { continent: "South America", rate: 4.2 },
    ],
    youth: [
      { continent: "Africa", rate: 8.2 },
      { continent: "Asia", rate: 10.1 },
      { continent: "Europe", rate: 11.7 },
      { continent: "North America", rate: 13.8 },
      { continent: "Oceania", rate: 14.5 },
      { continent: "South America", rate: 6.7 },
    ],
    domestic: [
      { continent: "Africa", rate: 9.0 },
      { continent: "Asia", rate: 10.5 },
      { continent: "Europe", rate: 12.0 },
      { continent: "North America", rate: 14.0 },
      { continent: "Oceania", rate: 15.0 },
      { continent: "South America", rate: 7.0 },
    ]
  };

  // Carte Leaflet
  const continentCenters = {
    Africa: [1.5, 17.0],
    Asia: [34.5, 100.0],
    Europe: [54.0, 15.0],
    "North America": [54.0, -105.0],
    Oceania: [-22.0, 140.0],
    "South America": [-14.0, -60.0]
  };

  let map = L.map("map").setView([20, 0], 2);

  // Tile Layer
  L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
    attribution:
      '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
  }).addTo(map);

  // Markers Layer Group (for easy clear)
  let markersLayer = L.layerGroup().addTo(map);

  // Function to update markers according to filter
  function updateMarkers(filter) {
    markersLayer.clearLayers();
    const data = suicideData[filter];
    data.forEach((item) => {
      const center = continentCenters[item.continent];
      if (!center) return;

      const rate = item.rate;
      // Color based on rate (scale from green to red)
      let color = "green";
      if (rate > 12) color = "red";
      else if (rate > 9) color = "orange";
      else if (rate > 6) color = "yellowgreen";

      const circle = L.circle(center, {
        color,
        fillColor: color,
        fillOpacity: 0.6,
        radius: rate * 30000 // radius proportional to rate
      }).addTo(markersLayer);

      circle.bindPopup(
        `<strong>${item.continent}</strong><br />Taux de suicide : ${rate} / 100 000 habitants`
      );
    });
  }

  // Initialize with "all"
  updateMarkers("all");

  // Filter buttons logic
  filterButtons.forEach(btn => {
    btn.addEventListener("click", () => {
      filterButtons.forEach(b => b.classList.remove("active"));
      btn.classList.add("active");
      updateMarkers(btn.getAttribute("data-filter"));
    });
  });

  // Paypal Button
  paypal.Buttons({
    style: {
      layout: 'horizontal',
      color:  'blue',
      shape:  'pill',
      label:  'donate'
    },
    createOrder: function(data, actions) {
      return actions.order.create({
        purchase_units: [{
          amount: {
            value: '5' // Valeur par défaut, peut être modifiée par l'utilisateur s'il est redirigé vers PayPal
          }
        }]
      });
    },
    onApprove: function(data, actions) {
      return actions.order.capture().then(function(details) {
        alert(`Merci pour votre don, ${details.payer.name.given_name}!`);
      });
    },
    onError: function(err) {
      alert('Erreur lors du paiement PayPal, veuillez réessayer.');
      console.error(err);
    }
  }).render('#paypal-button-container');

  // Initial language setup
  updateTexts(currentLang);
</script>
</body>
</html>

