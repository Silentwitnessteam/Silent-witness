<!DOCTYPE html>
<html lang="fr" dir="ltr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Silent Witness</title>

<!-- Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Cairo&family=Poppins:wght@400;700;900&display=swap" rel="stylesheet">

<style>
  :root {
    --color-primary: #1c5980;
    --color-secondary: #8fc1a1;
    --color-bg-light: #f9fafb;
    --color-bg-dark: #121212;
    --color-text-light: #1c1c1c;
    --color-text-dark: #e0e0e0;
    --transition-speed: 0.3s;
  }

  /* Reset & basics */
  * {
    box-sizing: border-box;
  }
  body {
    margin: 0; padding:0;
    font-family: 'Poppins', sans-serif;
    background-color: var(--color-bg-light);
    color: var(--color-text-light);
    transition: background-color var(--transition-speed), color var(--transition-speed);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  body.dark-theme {
    background-color: var(--color-bg-dark);
    color: var(--color-text-dark);
  }

  /* Header */
  header {
    background: var(--color-primary);
    color: white;
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  header .logo-container {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  header img.logo {
    height: 48px;
    border-radius: 6px;
  }
  header h1 {
    font-weight: 900;
    font-size: 1.8rem;
    margin: 0;
  }
  header .controls {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  select#lang-select {
    padding: 0.3rem 0.6rem;
    font-size: 1rem;
    border-radius: 6px;
    border: none;
    cursor: pointer;
  }
  button#theme-toggle {
    font-size: 1.4rem;
    background: transparent;
    border: none;
    color: white;
    cursor: pointer;
    transition: color 0.3s;
  }
  button#theme-toggle:hover {
    color: var(--color-secondary);
  }

  /* Main Title + animated text */
  #main-title-section {
    max-width: 900px;
    margin: 2rem auto 3rem;
    text-align: center;
  }
  #main-title-section h1 {
    font-size: 3rem;
    font-weight: 900;
    margin: 0 0 0.25rem 0;
    color: var(--color-primary);
    user-select: none;
  }
  #animated-text {
    font-size: 2.6rem;
    font-weight: 700;
    color: var(--color-secondary);
    user-select: none;
    animation: pulseText 2.5s infinite ease-in-out;
  }
  @keyframes pulseText {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.6; transform: scale(1.05); }
  }

  /* Donation Section */
  #donation-section {
    max-width: 380px;
    background: var(--color-primary);
    color: white;
    border-radius: 10px;
    padding: 1.5rem 2rem;
    margin: 2rem auto 4rem;
    box-shadow: 0 8px 20px rgba(28,89,128,0.4);
    text-align: center;
    user-select: none;
  }
  #donation-section h2 {
    margin-bottom: 1rem;
    font-size: 1.7rem;
    font-weight: 900;
  }
  #paypal-button-container {
    margin-top: 1rem;
  }

  /* White Paper Section */
  #whitepaper-section {
    max-width: 900px;
    margin: 0 auto 3rem;
    padding: 0 2rem;
    text-align: center;
  }
  #whitepaper-section p {
    font-size: 1.1rem;
    margin-bottom: 1rem;
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
  }
  #whitepaper-btn {
    display: inline-block;
    background: var(--color-primary);
    color: white;
    padding: 0.8rem 1.8rem;
    font-weight: 700;
    border-radius: 8px;
    text-decoration: none;
    transition: background-color 0.3s;
    user-select: none;
  }
  #whitepaper-btn:hover {
    background: var(--color-secondary);
    color: var(--color-primary);
  }

  /* Carte interactive Section */
  #map-section {
    max-width: 1100px;
    margin: 3rem auto 4rem;
    padding: 0 1rem;
  }
  #map-section h2 {
    text-align: center;
    font-weight: 900;
    font-size: 2rem;
    margin-bottom: 1rem;
    user-select: none;
  }
  #map {
    width: 100%;
    height: 550px;
    border-radius: 12px;
    box-shadow: 0 8px 16px rgba(28, 89, 128, 0.3);
  }
  /* Filter buttons */
  #filter-buttons {
    text-align: center;
    margin-bottom: 1rem;
  }
  #filter-buttons button {
    background: var(--color-primary);
    color: white;
    border: none;
    margin: 0 0.25rem;
    padding: 0.6rem 1rem;
    font-weight: 700;
    border-radius: 6px;
    cursor: pointer;
    transition: background-color 0.3s;
    user-select: none;
  }
  #filter-buttons button.active, #filter-buttons button:hover {
    background: var(--color-secondary);
    color: var(--color-primary);
  }

  /* Stats Section */
  #stats-section {
    max-width: 900px;
    margin: 0 auto 4rem;
    padding: 0 2rem;
  }
  #stats-section h2 {
    font-weight: 900;
    font-size: 2rem;
    margin-bottom: 1rem;
    user-select: none;
    text-align: center;
  }
  #stats-section ul {
    list-style: inside disc;
    font-size: 1.1rem;
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
    line-height: 1.6;
  }

  /* Detection Steps Section */
  #detection-steps {
    max-width: 900px;
    margin: 0 auto 4rem;
    padding: 0 2rem;
  }
  #detection-steps h2 {
    font-weight: 900;
    font-size: 2rem;
    margin-bottom: 1rem;
    text-align: center;
    user-select: none;
  }
  #detection-steps ol {
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
    font-size: 1.1rem;
    line-height: 1.6;
  }
  #detection-steps ol li {
    margin-bottom: 1rem;
    position: relative;
    padding-left: 2.2rem;
  }
  #detection-steps ol li::before {
    content: counter(step);
    counter-increment: step;
    position: absolute;
    left: 0;
    top: 0;
    background: var(--color-primary);
    color: white;
    width: 1.6rem;
    height: 1.6rem;
    border-radius: 50%;
    text-align: center;
    line-height: 1.6rem;
    font-weight: 900;
  }
  ol {
    counter-reset: step;
  }

  /* Contact Section */
  #contact-section {
    max-width: 600px;
    margin: 0 auto 3rem;
    padding: 0 1rem;
  }
  #contact-section h2 {
    font-weight: 900;
    font-size: 2rem;
    margin-bottom: 1rem;
    text-align: center;
    user-select: none;
  }
  form#contact-form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  form#contact-form input, form#contact-form textarea {
    padding: 0.8rem;
    border-radius: 6px;
    border: 1px solid #ccc;
    font-size: 1rem;
    font-family: inherit;
  }
  form#contact-form button {
    background: var(--color-primary);
    color: white;
    font-weight: 700;
    padding: 0.9rem;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  form#contact-form button:hover {
    background: var(--color-secondary);
    color: var(--color-primary);
  }

  /* Responsive */
  @media (max-width: 700px) {
    #main-title-section h1 {
      font-size: 2.2rem;
    }
    #animated-text {
      font-size: 1.8rem;
    }
    #map {
      height: 400px;
    }
    header {
      flex-direction: column;
      gap: 1rem;
    }
    header .controls {
      gap: 0.5rem;
    }
  }

  /* RTL Support for Arabic */
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

<!-- Leaflet CSS -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.3/dist/leaflet.css" />

</head>
<body>

<header>
  <div class="logo-container">
    <img src="https://cdn-icons-png.flaticon.com/512/1085/1085679.png" alt="IA et humain main dans la main" class="logo" />
    <h1>Silent Witness</h1>
  </div>
  <div class="controls">
    <select id="lang-select" aria-label="Choisir la langue">
      <option value="fr">🇫🇷 Français</option>
      <option value="en">🇬🇧 English</option>
      <option value="ar">🇸🇦 العربية</option>
    </select>
    <button id="theme-toggle" aria-label="Basculer thème clair/sombre">🌓</button>
  </div>
</header>

<section id="main-title-section" aria-label="Titre principal">
  <h1>Silent Witness</h1>
  <div id="animated-text" class="animated-text">Vous n'êtes pas seul</div>
</section>

<section id="donation-section" aria-label="Section de donation">
  <h2>Contribuez au projet Silent Witness</h2>
  <div id="paypal-button-container" aria-label="Bouton de donation PayPal"></div>
</section>

<section id="whitepaper-section" aria-label="Section White Paper">
  <p id="wp-paragraph"></p>
  <a id="whitepaper-btn" href="#" target="_blank" rel="noopener" class="download-btn"></a>
</section>

<section id="map-section" aria-label="Carte mondiale des suicides">
  <h2>Carte mondiale des suicides</h2>
  <div id="filter-buttons" role="group" aria-label="Filtres de la carte">
    <button data-filter="all" class="active">Tous</button>
    <button data-filter="men">Hommes</button>
    <button data-filter="women">Femmes</button>
    <button data-filter="youth">Jeunes</button>
    <button data-filter="domestic">Violences conjugales</button>
  </div>
  <div id="map"></div>
</section>

<section id="stats-section" aria-label="Statistiques clés">
  <h2>Statistiques clés</h2>
  <ul>
    <li>Près de 800 000 personnes se suicident chaque année (OMS)</li>
    <li>1 suicide toutes les 40 secondes dans le monde</li>
    <li>Le suicide est la 2e cause de mortalité chez les 15-29 ans</li>
    <li>Un nombre significatif de victimes sont liées aux violences conjugales</li>
  </ul>
</section>

<section id="detection-steps" aria-label="Étapes de détection IA">
  <h2>Étapes de détection IA</h2>
  <ol>
    <li>Analyse des mots clés dans les messages, requêtes IA ou recherches web</li>
    <li>Corrélation des données vocales, textuelles ou comportementales</li>
    <li>Évaluation automatique du niveau de détresse</li>
    <li>Classement de l’urgence (vert / orange / rouge)</li>
    <li>Déclenchement d'une alerte vers ONG, autorités ou hôpitaux selon le niveau</li>
  </ol>
</section>

<section id="contact-section" aria-label="Contact">
  <h2>Contactez-nous</h2>
  <form id="contact-form" aria-label="Formulaire de contact">
    <input type="text" name="nom" placeholder="Votre nom" required aria-required="true" />
    <input type="email" name="email" placeholder="Votre email" required aria-required="true" />
    <textarea name="message" rows="4" placeholder="Votre message" required aria-required="true"></textarea>
    <button type="submit">Envoyer</button>
  </form>
</section>

<!-- Scripts -->

<!-- Leaflet JS -->
<script src="https://unpkg.com/leaflet@1.9.3/dist/leaflet.js"></script>
<!-- EmailJS -->
<script src="https://cdn.emailjs.com/dist/email.min.js"></script>
<!-- PayPal SDK -->
<script src="https://www.paypal.com/sdk/js?client-id=BAAwNQmuQNtmwbB198XpnMFgJqBHvKNcvg138E9ddcIrNxHGCrGT2tvdVOyLaJTqde8dM-9e9ZglZUXS9A&currency=USD"></script>

<script>
  // EmailJS Init
  emailjs.init('_pR14KMi1syThzlmY');

  // Translations
  const translations = {
    fr: {
      animatedText: "Vous n'êtes pas seul",
      whitepaperText: "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.",
      whitepaperBtn: "📘 Télécharger notre White Paper",
      donationTitle: "Contribuez au projet Silent Witness",
      contactSendSuccess: "Message envoyé avec succès !",
      contactSendError: "Erreur lors de l'envoi, veuillez réessayer.",
      contactSubmitBtn: "Envoyer",
      donationCurrency: "USD",
      donationButtonText: "Faire un don",
    },
    en: {
      animatedText: "You're not alone",
      whitepaperText: "Explore our full white paper on Silent Witness – an ethical AI for prevention and protection of the vulnerable.",
      whitepaperBtn: "📘 Download our White Paper",
      donationTitle: "Support the Silent Witness Project",
      contactSendSuccess: "Message sent successfully!",
      contactSendError: "Error sending message, please try again.",
      contactSubmitBtn: "Send",
      donationCurrency: "USD",
      donationButtonText: "Donate",
    },
    ar: {
      animatedText: "لست وحدك",
      whitepaperText: "اكتشف الورقة البيضاء الخاصة بـ Silent Witness: ذكاء اصطناعي أخلاقي لحماية الفئات الأكثر عرضة للخطر.",
      whitepaperBtn: "📘 تحميل الورقة البيضاء",
      donationTitle: "ساهم في مشروع Silent Witness",
      contactSendSuccess: "تم إرسال الرسالة بنجاح!",
      contactSendError: "حدث خطأ أثناء الإرسال، يرجى المحاولة مرة أخرى.",
      contactSubmitBtn: "إرسال",
      donationCurrency: "USD",
      donationButtonText: "تبرع",
    }
  };

  // Set initial lang
  let currentLang = 'fr';

  // Update language function
  function updateLanguage(lang) {
    currentLang
