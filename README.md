<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Silent Witness - IA au service de l'humain</title>
  <style>
    /* Polices */
    @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&family=Cairo&display=swap');

    /* Reset & base */
    *, *::before, *::after {
      box-sizing: border-box;
    }
    body {
      margin: 0; padding: 0;
      font-family: 'Poppins', system-ui, sans-serif;
      background-color: #f9fafd;
      color: #1c5980;
      transition: background-color 0.3s ease, color 0.3s ease;
      line-height: 1.5;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    a {
      color: #1c5980;
      text-decoration: none;
    }
    a:hover, a:focus {
      text-decoration: underline;
      outline: none;
    }
    h1,h2,h3 {
      font-weight: 700;
      margin: 0.5rem 0 1rem 0;
      color: #1c5980;
    }
    button, select {
      font-family: inherit;
      font-size: 1rem;
      cursor: pointer;
    }

    /* Container */
    main {
      width: 95%;
      max-width: 1100px;
      margin: 1rem auto 3rem auto;
      flex: 1;
    }

    /* Header */
    header {
      width: 100%;
      background-color: #1c5980;
      color: white;
      padding: 1rem 1.5rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 1rem;
    }
    header h1 {
      margin: 0;
      font-size: 1.8rem;
      flex-grow: 1;
    }
    .controls {
      display: flex;
      gap: 1rem;
      align-items: center;
    }

    select#lang-select {
      padding: 0.25rem 0.5rem;
      border-radius: 6px;
      border: none;
      font-weight: 600;
      background-color: white;
      color: #1c5980;
      box-shadow: 0 0 5px rgba(28,89,128,0.2);
      min-width: 110px;
      appearance: none;
      -webkit-appearance: none;
      -moz-appearance: none;
      background-image: url('data:image/svg+xml;charset=US-ASCII,<svg xmlns="http://www.w3.org/2000/svg" width="10" height="5"><polygon points="0,0 10,0 5,5" fill="%231c5980"/></svg>');
      background-repeat: no-repeat;
      background-position: right 0.5rem center;
      background-size: 10px 5px;
    }

    button#theme-toggle {
      background: transparent;
      border: 2px solid white;
      color: white;
      padding: 0.25rem 0.6rem;
      border-radius: 6px;
      transition: background-color 0.3s ease, color 0.3s ease;
    }
    button#theme-toggle:hover, button#theme-toggle:focus {
      background-color: white;
      color: #1c5980;
      outline: none;
    }

    /* Hero section */
    #hero {
      text-align: center;
      padding: 3rem 1rem 4rem 1rem;
      background: linear-gradient(135deg, #8fc1a1cc 0%, #1c5980cc 100%);
      color: white;
      border-radius: 12px;
      box-shadow: 0 8px 20px rgb(28 89 128 / 0.3);
      margin-bottom: 3rem;
      position: relative;
    }
    #hero h2 {
      font-size: 2.8rem;
      margin-bottom: 0.5rem;
      font-family: 'Cairo', sans-serif;
      letter-spacing: 0.06em;
    }
    #hero .animated-text {
      font-weight: 900;
      animation: pulseText 2.5s infinite;
      display: inline-block;
      color: #daf0db;
      user-select: none;
    }
    #hero p {
      max-width: 650px;
      margin: 0 auto;
      font-size: 1.3rem;
      font-weight: 500;
    }

    @keyframes pulseText {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.6; transform: scale(1.1); }
    }

    /* Carousel */
    #visuals {
      margin-bottom: 3rem;
    }
    .carousel {
      max-width: 900px;
      margin: 0 auto;
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

    /* Workflow section */
    #workflow {
      max-width: 900px;
      margin: 3rem auto 4rem auto;
      font-family: 'Poppins', sans-serif;
      color: #1c5980;
    }
    #workflow h2 {
      text-align: center;
      font-size: 2.5rem;
      margin-bottom: 1rem;
    }
    #workflow p {
      font-size: 1.2rem;
      margin-bottom: 2rem;
      text-align: center;
    }
    #workflow ol {
      list-style-position: inside;
      font-size: 1.1rem;
      line-height: 1.6;
    }
    #workflow li {
      margin-bottom: 1rem;
    }
    #workflow ul {
      margin-top: 0.3rem;
      margin-left: 1.2rem;
    }
    #workflow strong {
      font-weight: 700;
      font-size: 1.15rem;
    }

    /* Statistics */
    #statistics {
      max-width: 900px;
      margin: 3rem auto 4rem auto;
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap;
      gap: 1.5rem;
      color: #1c5980;
    }
    .stat-card {
      background: #8fc1a1cc;
      border-radius: 10px;
      padding: 1.5rem 2rem;
      box-shadow: 0 3px 10px rgb(28 89 128 / 0.2);
      width: 250px;
      text-align: center;
      font-weight: 700;
      font-size: 2rem;
      user-select: none;
      transition: transform 0.3s ease;
    }
    .stat-card span.description {
      font-weight: 400;
      font-size: 1.1rem;
      display: block;
      margin-top: 0.6rem;
    }
    .stat-card:hover {
      transform: scale(1.07);
      box-shadow: 0 5px 15px rgb(28 89 128 / 0.35);
    }

    /* White Paper */
    #whitepaper {
      text-align: center;
      margin: 4rem auto;
      max-width: 700px;
    }
    #whitepaper h2 {
      font-size: 2rem;
      color: #1c5980;
      margin-bottom: 1rem;
      font-family: 'Poppins', sans-serif;
    }
    #whitepaper p {
      font-size: 1.2rem;
      color: #204d7a;
      margin-bottom: 1.5rem;
    }
    a.whitepaper-download-button {
      background-color: #1c5980;
      color: white;
      font-weight: bold;
      font-size: 1rem;
      padding: 12px 24px;
      border-radius: 10px;
      text-decoration: none;
      display: inline-block;
      margin-top: 1.5rem;
      transition: background-color 0.3s ease, transform 0.2s ease;
      user-select: none;
    }
    a.whitepaper-download-button:hover,
    a.whitepaper-download-button:focus {
      background-color: #8fc1a1;
      color: #1c5980;
      transform: scale(1.03);
      outline: none;
    }

    /* Contact Form */
    #contact {
      max-width: 700px;
      margin: 3rem auto 4rem auto;
      background: #daf0dbcc;
      border-radius: 12px;
      padding: 2rem;
      box-shadow: 0 8px 25px rgb(28 89 128 / 0.25);
    }
    #contact h2 {
      text-align: center;
      font-size: 2rem;
      color: #1c5980;
      margin-bottom: 1.5rem;
    }
    form label {
      display: block;
      margin-bottom: 0.3rem;
      font-weight: 600;
      color: #1c5980;
    }
    form input[type="text"],
    form input[type="email"],
    form textarea {
      width: 100%;
      padding: 0.6rem 0.8rem;
      border-radius: 6px;
      border: 1.5px solid #1c5980cc;
      font-size: 1rem;
      margin-bottom: 1rem;
      resize: vertical;
      font-family: inherit;
      transition: border-color 0.3s ease;
    }
    form input[type="text"]:focus,
    form input[type="email"]:focus,
    form textarea:focus {
      outline: none;
      border-color: #8fc1a1;
      box-shadow: 0 0 8px #8fc1a1cc;
    }
    form button[type="submit"] {
      background-color: #1c5980;
      color: white;
      font-weight: 700;
      font-size: 1.1rem;
      padding: 0.75rem 2rem;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: background-color 0.3s ease;
      user-select: none;
    }
    form button[type="submit"]:hover,
    form button[type="submit"]:focus {
      background-color: #8fc1a1;
      color: #1c5980;
      outline: none;
    }

    /* Footer */
    footer {
      width: 100%;
      padding: 1rem 1.5rem;
      background-color: #1c5980;
      color: white;
      text-align: center;
      font-size: 0.9rem;
      user-select: none;
    }

    /* Dark mode */
    body.dark {
      background-color: #121821;
      color: #a8c6d9;
    }
    body.dark header {
      background-color: #0f2c4e;
      color: #a8c6d9;
    }
    body.dark a {
      color: #8fc1a1;
    }
    body.dark a.whitepaper-download-button {
      background-color: #8fc1a1;
      color: #0f2c4e;
    }
    body.dark a.whitepaper-download-button:hover,
    body.dark a.whitepaper-download-button:focus {
      background-color: #1c5980;
      color: white;
    }
    body.dark #contact {
      background: #204d7a44;
      box-shadow: 0 8px 25px rgb(143 193 161 / 0.6);
    }
    body.dark form input[type="text"],
    body.dark form input[type="email"],
    body.dark form textarea {
      border-color: #8fc1a1cc;
      background-color: #1c5980;
      color: #daf0db;
    }
    body.dark form input[type="text"]:focus,
    body.dark form input[type="email"]:focus,
    body.dark form textarea:focus {
      box-shadow: 0 0 8px #daf0dbcc;
      border-color: #daf0dbcc;
      color: #daf0db;
    }
    body.dark form button[type="submit"] {
      background-color: #8fc1a1;
      color: #0f2c4e;
    }
    body.dark form button[type="submit"]:hover,
    body.dark form button[type="submit"]:focus {
      background-color: #1c5980;
      color: white;
    }
  </style>
</head>
<body>
  <header>
    <h1>Silent Witness</h1>
    <div class="controls">
      <label for="lang-select" class="visually-hidden">Choisir la langue</label>
      <select id="lang-select" aria-label="Choisir la langue">
        <option value="fr">Français</option>
        <option value="en">English</option>
        <option value="ar">العربية</option>
      </select>
      <button id="theme-toggle" aria-label="Changer le thème clair/sombre">🌙</button>
    </div>
  </header>

  <main>
    <section id="hero" aria-label="Présentation Silent Witness">
      <h2><span class="animated-text">You’re not alone</span></h2>
      <p data-i18n="hero-description">Silent Witness utilise l'intelligence artificielle pour détecter les signaux de détresse en temps réel et agir rapidement, en toute confidentialité.</p>
    </section>

    <!-- Carousel Images -->
    <section id="visuals" aria-label="Galerie images humain et technologie">
      <div class="carousel" aria-roledescription="carousel" aria-label="Images IA et humain">
        <button class="carousel-button prev" aria-label="Image précédente">&#10094;</button>
        <div class="carousel-track">
          <div class="carousel-slide">
            <img src="https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=900&q=80" alt="Visage humain en lumière douce" />
          </div>
          <div class="carousel-slide">
            <img src="https://images.unsplash.com/photo-1581093588401-2bcf4fbcfc1d?auto=format&fit=crop&w=900&q=80" alt="Schéma d'intelligence artificielle" />
          </div>
          <div class="carousel-slide">
            <img src="https://images.unsplash.com/photo-1517694712202-14dd9538aa97?auto=format&fit=crop&w=900&q=80" alt="Interaction entre humain et IA" />
          </div>
        </div>
        <button class="carousel-button next" aria-label="Image suivante">&#10095;</button>
        <div class="carousel-indicators" role="tablist" aria-label="Indicateurs des images">
          <button role="tab" aria-selected="true" aria-controls="slide1" id="indicator1" tabindex="0"></button>
          <button role="tab" aria-selected="false" aria-controls="slide2" id="indicator2" tabindex="-1"></button>
          <button role="tab" aria-selected="false" aria-controls="slide3" id="indicator3" tabindex="-1"></button>
        </div>
      </div>
    </section>

    <!-- Pipeline / Workflow -->
    <section id="workflow" tabindex="0" aria-label="Pipeline de détection Silent Witness">
      <h2 data-i18n="pipeline-title">Pipeline de détection Silent Witness</h2>
      <p data-i18n="pipeline-description">
        Voici le workflow innovant et éthique de notre système Silent Witness, conçu pour détecter, analyser et alerter en cas de détresse en temps réel.
      </p>
      <ol>
        <li>
          <strong data-i18n="step1-title">Capture & Pré-traitement des données</strong>
          <ul>
            <li data-i18n="step1-1">Collecte en temps réel des messages, sons, textes, recherches et mouvements.</li>
            <li data-i18n="step1-2">Nettoyage automatique et anonymisation des données.</li>
            <li data-i18n="step1-3">Segmentation en unités analytiques.</li>
          </ul>
        </li>
        <li>
          <strong data-i18n="step2-title">Analyse sémantique & détection de mots-clés</strong>
          <ul>
            <li data-i18n="step2-1">Utilisation d’un modèle NLP spécialisé pour identifier mots clés et contextes liés à la détresse.</li>
            <li data-i18n="step2-2">Analyse fine de la tonalité émotionnelle.</li>
            <li data-i18n="step2-3">Score initial de détresse et liste des mots/expressions clés détectés.</li>
          </ul>
        </li>
        <li>
          <strong data-i18n="step3-title">Enrichissement par recherches web & contexte</strong>
          <ul>
            <li data-i18n="step3-1">Recherche automatique d’informations complémentaires pour valider et contextualiser les signaux.</li>
            <li data-i18n="step3-2">Prise en compte des actualités locales et événements récents.</li>
            <li data-i18n="step3-3">Score ajusté et lien vers les sources.</li>
          </ul>
        </li>
        <li>
          <strong data-i18n="step4-title">Classification & hiérarchisation des alertes</strong>
          <ul>
            <li data-i18n="step4-1">Classement en niveaux de gravité (Surveillance, Alerte modérée, Alerte critique).</li>
            <li data-i18n="step4-2">Prise en compte des historiques et facteurs additionnels.</li>
          </ul>
        </li>
        <li>
          <strong data-i18n="step5-title">Constitution du dossier d’alerte & validation éthique</strong>
          <ul>
            <li data-i18n="step5-1">Compilation des données horodatées, analyses et suggestions d’intervention.</li>
            <li data-i18n="step5-2">Filtrage par module de contrôle éthique pour garantir confidentialité et pertinence.</li>
          </ul>
        </li>
        <li>
          <strong data-i18n="step6-title">Transmission & suivi</strong>
          <ul>
            <li data-i18n="step6-1">Envoi sécurisé du dossier aux entités concernées selon le niveau d’alerte.</li>
            <li data-i18n="step6-2">Notification adaptée à la personne en détresse.</li>
            <li data-i18n="step6-3">Suivi en temps réel du dossier.</li>
          </ul>
        </li>
        <li>
          <strong data-i18n="step7-title">Apprentissage continu</strong>
          <ul>
            <li data-i18n="step7-1">Amélioration grâce aux retours des intervenants.</li>
            <li data-i18n="step7-2">Affinement des modèles IA et règles contextuelles.</li>
            <li data-i18n="step7-3">Adaptation locale culturelle et linguistique.</li>
          </ul>
        </li>
      </ol>
    </section>

    <!-- Statistiques -->
    <section id="statistics" aria-label="Statistiques du projet Silent Witness" role="region" aria-live="polite">
      <div class="stat-card" tabindex="0" aria-label="Plus de 5000 alertes détectées">
        5,000+<span class="description" data-i18n="stats-alerts">Alertes détectées</span>
      </div>
      <div class="stat-card" tabindex="0" aria-label="98 pour cent de précision de détection">
        98%<span class="description" data-i18n="stats-precision">Précision de détection</span>
      </div>
      <div class="stat-card" tabindex="0" aria-label="Plus de 200 interventions réalisées">
        200+<span class="description" data-i18n="stats-interventions">Interventions réalisées</span>
      </div>
      <div class="stat-card" tabindex="0" aria-label="24 heures sur 24, disponibilité active">
        24/7<span class="description" data-i18n="stats-availability">Disponibilité active</span>
      </div>
    </section>

    <!-- White Paper -->
    <section id="whitepaper" aria-label="Téléchargement du White Paper Silent Witness">
      <h2 data-i18n="whitepaper-title">Téléchargez notre White Paper</h2>
      <p data-i18n="whitepaper-desc">Découvrez en détail la technologie, l’éthique et les étapes du projet Silent Witness.</p>
      <a href="SilentWitness_WhitePaper_FR.pdf" download class="whitepaper-download-button" aria-label="Télécharger le White Paper en Français">📄 Français</a>
      <a href="SilentWitness_WhitePaper_EN.pdf" download class="whitepaper-download-button" aria-label="Download White Paper in English" style="margin-left: 1rem;">📄 English</a>
      <a href="SilentWitness_WhitePaper_AR.pdf" download class="whitepaper-download-button" aria-label="تحميل الورقة البيضاء بالعربية" style="margin-left: 1rem;">📄 العربية</a>
    </section>

    <!-- Contact Form -->
    <section id="contact" aria-label="Formulaire de contact">
      <h2 data-i18n="contact-title">Contactez-nous</h2>
      <form id="contact-form" aria-live="polite" aria-relevant="additions" novalidate>
        <label for="name" data-i18n="contact-name">Nom complet</label>
        <input type="text" id="name" name="user_name" required autocomplete="name" aria-required="true" />

        <label for="email" data-i18n="contact-email">Adresse e-mail</label>
        <input type="email" id="email" name="user_email" required autocomplete="email" aria-required="true" />

        <label for="message" data-i18n="contact-message">Message</label>
        <textarea id="message" name="message" rows="5" required aria-required="true"></textarea>

        <button type="submit" aria-live="assertive" aria-atomic="true" data-i18n="contact-send">Envoyer</button>
      </form>
      <p id="form-status" role="alert" aria-live="assertive" style="margin-top: 1rem; color: #1c5980; font-weight: 600;"></p>
    </section>
  </main>

  <footer>
    <p>© 2025 Silent Witness - Tous droits réservés</p>
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/emailjs-com@3/dist/email.min.js"></script>
  <script>
    // Initialisation EmailJS
    emailjs.init('_pR14KMi1syThzlmY');

    // Gestion formulaire
    const form = document.getElementById('contact-form');
    const status = document.getElementById('form-status');
    form.addEventListener('submit', function (e) {
      e.preventDefault();
      status.textContent = '';
      // Validation basique
      if(!form.user_name.value.trim() || !form.user_email.value.trim() || !form.message.value.trim()) {
        status.textContent = translations[currentLang].formError || 'Veuillez remplir tous les champs.';
        return;
      }
      emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', this)
        .then(() => {
          status.style.color = '#1c5980';
          status.textContent = translations[currentLang].formSuccess || 'Message envoyé avec succès !';
          form.reset();
        }, (error) => {
          status.style.color = 'red';
          status.textContent = translations[currentLang].formErrorSend || 'Erreur lors de l\'envoi, réessayez.';
          console.error(error);
        });
    });

    // Gestion carousel simple
    const track = document.querySelector('.carousel-track');
    const slides = Array.from(track.children);
    const nextButton = document.querySelector('.carousel-button.next');
    const prevButton = document.querySelector('.carousel-button.prev');
    const indicators = document.querySelectorAll('.carousel-indicators button');

    let currentIndex = 0;
    function updateCarousel(index) {
      if(index < 0) index = slides.length - 1;
      if(index >= slides.length) index = 0;
      currentIndex = index;
      const amountToMove = -index * 100;
      track.style.transform = `translateX(${amountToMove}%)`;

      indicators.forEach((btn, i) => {
        btn.setAttribute('aria-selected', i === index ? 'true' : 'false');
        btn.tabIndex = i === index ? 0 : -1;
      });
    }
    nextButton.addEventListener('click', () => updateCarousel(currentIndex + 1));
    prevButton.addEventListener('click', () => updateCarousel(currentIndex - 1));
    indicators.forEach((btn, i) => {
      btn.addEventListener('click', () => updateCarousel(i));
      btn.addEventListener('keydown', (e) => {
        if(e.key === 'Enter' || e.key === ' ') {
          e.preventDefault();
          updateCarousel(i);
        }
      });
    });
    updateCarousel(0);

    // Thème clair / sombre
    const themeToggle = document.getElementById('theme-toggle');
    const body = document.body;

    function updateTheme() {
      if(localStorage.getItem('theme') === 'dark') {
        body.classList.add('dark');
        themeToggle.textContent = '☀️';
      } else {
        body.classList.remove('dark');
        themeToggle.textContent = '🌙';
      }
    }
    themeToggle.addEventListener('click', () => {
      if(body.classList.contains('dark')) {
        localStorage.setItem('theme', 'light');
      } else {
        localStorage.setItem('theme', 'dark');
      }
      updateTheme();
    });
    updateTheme();

    // Gestion multilingue simplifiée
    const translations = {
      fr: {
        'hero-description': "Silent Witness utilise l'intelligence artificielle pour détecter les signaux de détresse en temps réel et agir rapidement, en toute confidentialité.",
        'pipeline-title': "Pipeline de détection Silent Witness",
        'pipeline-description': "Voici le workflow innovant et éthique de notre système Silent Witness, conçu pour détecter, analyser et alerter en cas de détresse en temps réel.",
        'step1-title': "Capture & Pré-traitement des données",
        'step1-1': "Collecte en temps réel des messages, sons, textes, recherches et mouvements.",
        'step1-2': "Nettoyage automatique et anonymisation des données.",
        'step1-3': "Segmentation en unités analytiques.",
        'step2-title': "Analyse sémantique & détection de mots-clés",
        'step2-1': "Utilisation d’un modèle NLP spécialisé pour identifier mots clés et contextes liés à la détresse.",
        'step2-2': "Analyse fine de la tonalité émotionnelle.",
        'step2-3': "Score initial de détresse et liste des mots/expressions clés détectés.",
        'step3-title': "Enrichissement par recherches web & contexte",
        'step3-1': "Recherche automatique d’informations complémentaires pour valider et contextualiser les signaux.",
        'step3-2': "Prise en compte des actualités locales et événements récents.",
        'step3-3': "Score ajusté et lien vers les sources.",
        'step4-title': "Classification & hiérarchisation des alertes",
        'step4-1': "Classement en niveaux de gravité (Surveillance, Alerte modérée, Alerte critique).",
        'step4-2': "Prise en compte des historiques et facteurs additionnels.",
        'step5-title': "Constitution du dossier d’alerte & validation éthique",
        'step5-1': "Compilation des données horodatées, analyses et suggestions d’intervention.",
        'step5-2': "Filtrage par module de contrôle éthique pour garantir confidentialité et pertinence.",
        'step6-title': "Transmission & suivi",
        'step6-1': "Envoi sécurisé du dossier aux entités concernées selon le niveau d’alerte.",
        'step6-2': "Notification adaptée à la personne en détresse.",
        'step6-3': "Suivi en temps réel du dossier.",
        'step7-title': "Apprentissage continu",
        'step7-1': "Amélioration grâce aux retours des intervenants.",
        'step7-2': "Affinement des modèles IA et règles contextuelles.",
        'step7-3': "Adaptation locale culturelle et linguistique.",
        'stats-alerts': "Alertes détectées",
        'stats-precision': "Précision de détection",
        'stats-interventions': "Interventions réalisées",
        'stats-availability': "Disponibilité active",
        'whitepaper-title': "Téléchargez notre White Paper",
        'whitepaper-desc': "Découvrez en détail la technologie, l’éthique et les étapes du projet Silent Witness.",
        'contact-title': "Contactez-nous",
        'contact-name': "Nom complet",
        'contact-email': "Adresse e-mail",
        'contact-message': "Message",
        'contact-send': "Envoyer",
        'formSuccess': "Message envoyé avec succès !",
        'formError': "Veuillez remplir tous les champs.",
        'formErrorSend': "Erreur lors de l'envoi, réessayez."
      },
      en: {
        'hero-description': "Silent Witness uses artificial intelligence to detect distress signals in real time and act quickly with full confidentiality.",
        'pipeline-title': "Silent Witness Detection Pipeline",
        'pipeline-description': "Here is the innovative and ethical workflow of our Silent Witness system, designed to detect, analyze, and alert in case of distress in real time.",
        'step1-title': "Data Capture & Preprocessing",
        'step1-1': "Real-time collection of messages, sounds, texts, searches, and movements.",
        'step1-2': "Automatic data cleaning and anonymization.",
        'step1-3': "Segmentation into analytical units.",
        'step2-title': "Semantic Analysis & Keyword Detection",
        'step2-1': "Use of a specialized NLP model to identify keywords and contexts related to distress.",
        'step2-2': "Fine emotional tone analysis.",
        'step2-3': "Initial distress score and list of detected keywords/expressions.",
        'step3-title': "Enrichment via Web Searches & Context",
        'step3-1': "Automatic research of complementary information to validate and contextualize signals.",
        'step3-2': "Consideration of local news and recent events.",
        'step3-3': "Adjusted score and link to sources.",
        'step4-title': "Alert Classification & Prioritization",
        'step4-1': "Classification into severity levels (Monitoring, Moderate Alert, Critical Alert).",
        'step4-2': "Consideration of histories and additional factors.",
        'step5-title': "Alert Dossier Compilation & Ethical Validation",
        'step5-1': "Compilation of timestamped data, analyses and intervention suggestions.",
        'step5-2': "Filtering by ethical control module to guarantee confidentiality and relevance.",
        'step6-title': "Transmission & Follow-up",
        'step6-1': "Secure sending of the dossier to concerned entities according to alert level.",
        'step6-2': "Notification adapted to the person in distress.",
        'step6-3': "Real-time dossier tracking.",
        'step7-title': "Continuous Learning",
        'step7-1': "Improvement based on feedback from responders.",
        'step7-2': "Refinement of AI models and contextual rules.",
        'step7-3': "Local cultural and linguistic adaptation.",
        'stats-alerts': "Alerts detected",
        'stats-precision': "Detection accuracy",
        'stats-interventions': "Interventions performed",
        'stats-availability': "Active availability",
        'whitepaper-title': "Download our White Paper",
        'whitepaper-desc': "Discover in detail the technology, ethics, and steps of the Silent Witness project.",
        'contact-title': "Contact us",
        'contact-name': "Full name",
        'contact-email': "Email address",
        'contact-message': "Message",
        'contact-send': "Send",
        'formSuccess': "Message sent successfully!",
        'formError': "Please fill out all fields.",
        'formErrorSend': "Error sending message, please try again."
      },
      ar: {
        'hero-description': "يستخدم شاهد صامت الذكاء الاصطناعي للكشف عن إشارات distress في الوقت الحقيقي واتخاذ الإجراءات بسرعة مع الحفاظ على السرية الكاملة.",
        'pipeline-title': "خط أنابيب الكشف لشاهد صامت",
        'pipeline-description': "إليك سير العمل المبتكر والأخلاقي لنظام شاهد صامت، المصمم للكشف والتحليل والتنبيه في حالة وجود distress في الوقت الحقيقي.",
        'step1-title': "جمع البيانات والمعالجة الأولية",
        'step1-1': "جمع الرسائل والأصوات والنصوص والبحث والحركات في الوقت الحقيقي.",
        'step1-2': "تنظيف البيانات التلقائي وإخفاء الهوية.",
        'step1-3': "تقسيم البيانات إلى وحدات تحليلية.",
        'step2-title': "التحليل الدلالي واكتشاف الكلمات المفتاحية",
        'step2-1': "استخدام نموذج معالجة لغة طبيعية متخصص لتحديد الكلمات المفتاحية والسياقات المتعلقة بالضيق.",
        'step2-2': "تحليل دقيق للنبرة العاطفية.",
        'step2-3': "درجة مبدئية للضيق وقائمة بالكلمات/العبارات المفتاحية المكتشفة.",
        'step3-title': "التعزيز عبر البحث على الويب والسياق",
        'step3-1': "البحث التلقائي عن معلومات إضافية للتحقق وتوفير السياق للإشارات.",
        'step3-2': "أخذ الأخبار المحلية والأحداث الحديثة في الاعتبار.",
        'step3-3': "تعديل الدرجة والرابط للمصادر.",
        'step4-title': "تصنيف وتنظيم التنبيهات",
        'step4-1': "تصنيف إلى مستويات شدة (المراقبة، تنبيه متوسط، تنبيه حرج).",
        'step4-2': "أخذ التاريخ والعوامل الإضافية في الاعتبار.",
        'step5-title': "تجميع ملف التنبيه والتحقق الأخلاقي",
        'step5-1': "تجميع البيانات المؤرخة، التحليلات، واقتراحات التدخل.",
        'step5-2': "الترشيح عبر وحدة التحكم الأخلاقية لضمان السرية والأهمية.",
        'step6-title': "الإرسال والمتابعة",
        'step6-1': "إرسال آمن للملف إلى الجهات المعنية حسب مستوى التنبيه.",
        'step6-2': "إشعار مناسب للشخص في حالة الضيق.",
        'step6-3': "المتابعة في الوقت الحقيقي للملف.",
        'step7-title': "التعلم المستمر",
        'step7-1': "التحسين بناءً على ملاحظات المستجيبين.",
        'step7-2': "تحسين نماذج الذكاء الاصطناعي والقواعد السياقية.",
        'step7-3': "التكيف الثقافي واللغوي المحلي.",
        'stats-alerts': "التنبيهات المكتشفة",
        'stats-precision': "دقة الكشف",
        'stats-interventions': "التدخلات المنفذة",
        'stats-availability': "التوفر النشط",
        'whitepaper-title': "قم بتنزيل الورقة البيضاء",
        'whitepaper-desc': "اكتشف بالتفصيل التكنولوجيا والأخلاقيات وخطوات مشروع شاهد صامت.",
        'contact-title': "اتصل بنا",
        'contact-name': "الاسم الكامل",
        'contact-email': "البريد الإلكتروني",
        'contact-message': "الرسالة",
        'contact-send': "إرسال",
        'formSuccess': "تم إرسال الرسالة بنجاح!",
        'formError': "يرجى ملء جميع الحقول.",
        'formErrorSend': "حدث خطأ أثناء الإرسال، يرجى المحاولة مرة أخرى."
      }
    };

    const langSelect = document.getElementById('lang-select');
    let currentLang = localStorage.getItem('lang') || 'fr';

    function updateTranslations(lang) {
      document.querySelectorAll('[data-i18n]').forEach(el => {
        const key = el.getAttribute('data-i18n');
        if(translations[lang] && translations[lang][key]) {
          el.textContent = translations[lang][key];
        }
      });
    }
    // Set default language selection
    langSelect.value = currentLang;
    updateTranslations(currentLang);

    langSelect.addEventListener('change', (e) => {
      currentLang = e.target.value;
      localStorage.setItem('lang', currentLang);
      updateTranslations(currentLang);
    });
  </script>
</body>
</html>

