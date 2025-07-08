<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Silent Witness - IA au service de l'humain</title>

<!-- Polices -->
<link href="https://fonts.googleapis.com/css2?family=Cairo&family=Poppins&display=swap" rel="stylesheet" />

<style>
  /* RESET et bases */
  * {
    box-sizing: border-box;
  }
  body {
    margin: 0; padding: 0;
    font-family: 'Poppins', 'Cairo', system-ui, sans-serif;
    background-color: #f9f9f9;
    color: #1c5980;
    transition: background-color 0.3s, color 0.3s;
  }
  body.dark {
    background-color: #121618;
    color: #a0cbb8;
  }
  a {
    color: #1c5980;
    text-decoration: none;
  }
  a:hover, a:focus {
    color: #8fc1a1;
  }
  header {
    background-color: #1c5980;
    color: white;
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
  }
  header.dark {
    background-color: #0f2c25;
  }
  .logo {
    font-weight: 700;
    font-size: 1.5rem;
  }

  /* Sélecteur langues */
  #language-select {
    font-size: 1rem;
    padding: 0.3rem 0.5rem;
    border-radius: 6px;
    border: none;
    cursor: pointer;
  }
  #language-select:focus {
    outline: 2px solid #8fc1a1;
  }

  /* Toggle fond clair/sombre */
  #theme-toggle {
    margin-left: 1rem;
    cursor: pointer;
    background: none;
    border: 2px solid white;
    border-radius: 20px;
    width: 38px;
    height: 22px;
    position: relative;
  }
  #theme-toggle::before {
    content: "";
    position: absolute;
    width: 18px;
    height: 18px;
    background: white;
    border-radius: 50%;
    top: 1px;
    left: 1px;
    transition: left 0.3s;
  }
  body.dark #theme-toggle::before {
    left: 19px;
    background: #1c5980;
  }

  /* Section Hero */
  #hero {
    text-align: center;
    padding: 5rem 1rem 3rem;
  }
  #hero h1 {
    font-size: 2.8rem;
    margin-bottom: 1rem;
    font-weight: 700;
  }
  #hero h2 {
    font-size: 1.8rem;
    color: #8fc1a1;
    font-weight: 600;
    height: 2.5rem;
    overflow: hidden;
    white-space: nowrap;
    border-right: 4px solid #1c5980;
    margin: 0 auto;
    width: max-content;
    animation: typing 3s steps(25) infinite alternate;
  }
  @keyframes typing {
    0% { width: 0; }
    50% { width: 20ch; }
    100% { width: 0; }
  }

  /* Carousel */
  #visuals {
    max-width: 900px;
    margin: 3rem auto;
    padding: 0 1rem;
  }
  .carousel {
    overflow: hidden;
    border-radius: 12px;
    box-shadow: 0 5px 15px rgba(28,89,128,0.3);
    background: white;
    position: relative;
    user-select: none;
  }
  .carousel-track {
    display: flex;
    transition: transform 0.5s ease;
    will-change: transform;
  }
  .carousel-slide {
    min-width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .carousel-slide img {
    width: 100%;
    max-height: 400px;
    object-fit: cover;
    border-radius: 12px;
    pointer-events: none;
  }
  .carousel-button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: #1c5980cc;
    border: none;
    color: white;
    font-size: 2.5rem;
    padding: 0.3rem 1rem;
    cursor: pointer;
    border-radius: 50%;
    transition: background-color 0.3s ease;
    user-select: none;
    z-index: 10;
  }
  .carousel-button:hover,
  .carousel-button:focus {
    background: #8fc1a1cc;
    color: #1c5980;
    outline: none;
  }
  .carousel-button.prev {
    left: 15px;
  }
  .carousel-button.next {
    right: 15px;
  }
  .carousel-indicators {
    position: absolute;
    bottom: 15px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    gap: 10px;
  }
  .carousel-indicators button {
    width: 14px;
    height: 14px;
    background: #ccc;
    border-radius: 50%;
    border: none;
    cursor: pointer;
  }
  .carousel-indicators button[aria-selected="true"] {
    background: #1c5980;
  }
  body.dark .carousel {
    background: #1b2d30;
    box-shadow: 0 5px 20px rgba(143,193,161,0.3);
  }

  /* Section statistiques */
  #statistics {
    max-width: 900px;
    margin: 3rem auto;
    padding: 0 1rem;
    display: flex;
    justify-content: space-around;
    gap: 1rem;
    flex-wrap: wrap;
  }
  .stat-card {
    background: white;
    border-radius: 12px;
    padding: 1.5rem 2rem;
    text-align: center;
    flex: 1 1 250px;
    box-shadow: 0 3px 8px rgba(28,89,128,0.15);
    transition: background-color 0.3s, color 0.3s;
  }
  .stat-card h3 {
    font-size: 2.5rem;
    margin: 0;
    color: #1c5980;
  }
  .stat-card p {
    font-size: 1.2rem;
    margin-top: 0.3rem;
    font-weight: 600;
  }
  body.dark .stat-card {
    background: #1b2d30;
    color: #a0cbb8;
  }

  /* Section White Paper */
  #whitepaper {
    text-align: center;
    margin: 4rem auto;
    max-width: 600px;
    padding: 0 1rem;
  }
  #whitepaper h2 {
    font-size: 2rem;
    color: #1c5980;
    margin-bottom: 0.5rem;
  }
  #whitepaper p {
    font-size: 1.2rem;
    color: #204d7a;
    margin-bottom: 1.5rem;
  }
  #whitepaper a.whitepaper-download-button {
    background-color: #1c5980;
    color: white;
    font-weight: bold;
    font-size: 1rem;
    padding: 12px 24px;
    border-radius: 10px;
    text-decoration: none;
    display: inline-block;
    transition: background-color 0.3s ease, transform 0.2s ease;
  }
  #whitepaper a.whitepaper-download-button:hover,
  #whitepaper a.whitepaper-download-button:focus {
    background-color: #8fc1a1;
    color: #1c5980;
    transform: scale(1.03);
  }
  body.dark #whitepaper h2 {
    color: #8fc1a1;
  }
  body.dark #whitepaper p {
    color: #a0cbb8;
  }

  /* Formulaire contact */
  #contact {
    max-width: 600px;
    margin: 4rem auto 6rem;
    padding: 0 1rem;
  }
  #contact h2 {
    text-align: center;
    font-size: 2rem;
    margin-bottom: 2rem;
    color: #1c5980;
  }
  #contact form {
    display: flex;
    flex-direction: column;
    gap: 1.3rem;
  }
  #contact label {
    font-weight: 600;
  }
  #contact input, #contact textarea {
    padding: 0.7rem;
    font-size: 1rem;
    border-radius: 6px;
    border: 1.5px solid #8fc1a1;
    resize: vertical;
    transition: border-color 0.3s ease;
    font-family: 'Poppins', sans-serif;
  }
  #contact input:focus, #contact textarea:focus {
    border-color: #1c5980;
    outline: none;
  }
  #contact button {
    background-color: #1c5980;
    color: white;
    font-weight: 700;
    padding: 0.8rem 0;
    font-size: 1.2rem;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  #contact button:hover,
  #contact button:focus {
    background-color: #8fc1a1;
    color: #1c5980;
    outline: none;
  }
  /* Responsive */
  @media (max-width: 720px) {
    #statistics {
      flex-direction: column;
      align-items: center;
    }
    .stat-card {
      width: 80%;
    }
  }
</style>
</head>

<body>

<header id="header">
  <div class="logo" tabindex="0">Silent Witness</div>
  <div>
    <select id="language-select" aria-label="Sélecteur de langue">
      <option value="fr" selected>Français</option>
      <option value="en">English</option>
      <option value="ar">العربية</option>
    </select>
    <button id="theme-toggle" aria-label="Changer thème clair/sombre" title="Changer thème clair/sombre"></button>
  </div>
</header>

<section id="hero" role="banner" aria-label="Introduction">
  <h1 data-i18n="heroTitle">Silent Witness</h1>
  <h2 class="animated-text" data-i18n="heroSubtitle">You're not alone</h2>
</section>

<section id="visuals" tabindex="0" aria-label="Galerie images humain et technologie">
  <h2 data-i18n="visualsTitle">Humain & Technologie</h2>
  <div class="carousel" aria-live="polite" aria-roledescription="carousel">
    <button class="carousel-button prev" aria-label="Image précédente" aria-controls="carousel-track" aria-disabled="false">&#10094;</button>
    <div class="carousel-track" id="carousel-track">
      <div class="carousel-slide" role="group" aria-roledescription="slide" aria-label="Image 1 sur 3">
        <img src="https://images.unsplash.com/photo-1518770660439-4636190af475?auto=format&fit=crop&w=800&q=80" alt="Visage humain et visage robot en transparence" />
      </div>
      <div class="carousel-slide" role="group" aria-roledescription="slide" aria-label="Image 2 sur 3">
        <img src="https://images.unsplash.com/photo-1497493292307-31c376b6e479?auto=format&fit=crop&w=800&q=80" alt="Femme et robot collaborant ensemble" />
      </div>
      <div class="carousel-slide" role="group" aria-roledescription="slide" aria-label="Image 3 sur 3">
        <img src="https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=800&q=80" alt="Homme avec un casque de réalité augmentée" />
      </div>
    </div>
    <button class="carousel-button next" aria-label="Image suivante" aria-controls="carousel-track" aria-disabled="false">&#10095;</button>

    <div class="carousel-indicators" role="tablist" aria-label="Indicateurs de position">
      <button role="tab" aria-selected="true" aria-controls="slide1" id="indicator1" tabindex="0"></button>
      <button role="tab" aria-selected="false" aria-controls="slide2" id="indicator2" tabindex="-1"></button>
      <button role="tab" aria-selected="false" aria-controls="slide3" id="indicator3" tabindex="-1"></button>
    </div>
  </div>
</section>

<section id="statistics" aria-label="Statistiques">
  <div class="stat-card" tabindex="0">
    <h3 data-i18n="stat1Number">95%</h3>
    <p data-i18n="stat1Text">Détection précoce des signaux de détresse</p>
  </div>
  <div class="stat-card" tabindex="0">
    <h3 data-i18n="stat2Number">1500+</h3>
    <p data-i18n="stat2Text">Signaux analysés chaque jour</p>
  </div>
  <div class="stat-card" tabindex="0">
    <h3 data-i18n="stat3Number">98%</h3>
    <p data-i18n="stat3Text">Précision des alertes transmises</p>
  </div>
</section>

<section id="whitepaper" tabindex="0" aria-label="Téléchargement White Paper">
  <h2 id="whitepaper-title" data-i18n="whitepaperTitle">You're not alone</h2>
  <p id="whitepaper-desc" data-i18n="whitepaperDesc">
    Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.
  </p>
  <a
    id="whitepaper-button"
    href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf"
    target="_blank"
    class="whitepaper-download-button"
    data-i18n="whitepaperButton"
    >📘 Télécharger notre White Paper</a
  >
</section>

<section id="contact" aria-label="Formulaire de contact">
  <h2 data-i18n="contactTitle">Contactez-nous</h2>
  <form id="contact-form" aria-describedby="contact-instructions">
    <p id="contact-instructions" class="sr-only">
      Remplissez le formulaire pour nous envoyer un message. Tous les champs sont obligatoires.
    </p>
    <label for="nom" data-i18n="labelName">Nom :</label>
    <input type="text" id="nom" name="nom" required aria-required="true" />

    <label for="email" data-i18n="labelEmail">Email :</label>
    <input type="email" id="email" name="email" required aria-required="true" />

    <label for="message" data-i18n="labelMessage">Message :</label>
    <textarea id="message" name="message" rows="5" required aria-required="true"></textarea>

    <button type="submit" data-i18n="btnSend">Envoyer</button>
  </form>
  <p id="form-status" role="alert" aria-live="polite" style="margin-top:1rem;"></p>
</section>

<script src="https://cdn.emailjs.com/dist/email.min.js"></script>
<script>
  emailjs.init('_pR14KMi1syThzlmY');
</script>

<script>
  // Texte multilingue
  const translations = {
    fr: {
      heroTitle: "Silent Witness",
      heroSubtitle: "Vous n'êtes pas seul",
      visualsTitle: "Humain & Technologie",
      stat1Number: "95%",
      stat1Text: "Détection précoce des signaux de détresse",
      stat2Number: "1500+",
      stat2Text: "Signaux analysés chaque jour",
      stat3Number: "98%",
      stat3Text: "Précision des alertes transmises",
      whitepaperTitle: "Vous n'êtes pas seul",
      whitepaperDesc:
        "Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.",
      whitepaperButton: "📘 Télécharger notre White Paper",
      contactTitle: "Contactez-nous",
      labelName: "Nom :",
      labelEmail: "Email :",
      labelMessage: "Message :",
      btnSend: "Envoyer",
      sendSuccess: "Message envoyé avec succès ! Merci.",
      sendError: "Erreur lors de l'envoi, veuillez réessayer.",
    },
    en: {
      heroTitle: "Silent Witness",
      heroSubtitle: "You're not alone",
      visualsTitle: "Human & Technology",
      stat1Number: "95%",
      stat1Text: "Early detection of distress signals",
      stat2Number: "1500+",
      stat2Text: "Signals analyzed daily",
      stat3Number: "98%",
      stat3Text: "Accuracy of alerts sent",
      whitepaperTitle

