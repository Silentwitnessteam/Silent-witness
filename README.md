<!DOCTYPE html>
<html lang="fr" dir="ltr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Silent Witness - IA au service de l'humain</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet" />
  <style>
    /* Reset & global */
    * {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: #f5f7fa;
      color: #1c5980;
      line-height: 1.5;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }
    header {
      background-color: #1c5980;
      color: white;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-shrink: 0;
    }
    header strong {
      font-size: 1.5rem;
      user-select: none;
    }
    .visually-hidden {
      position: absolute !important;
      width: 1px;
      height: 1px;
      padding: 0;
      margin: -1px;
      overflow: hidden;
      clip: rect(0, 0, 0, 0);
      border: 0;
    }
    .lang-select {
      font-family: 'Poppins', sans-serif;
      font-weight: 600;
      font-size: 1rem;
      color: #1c5980;
      background-color: white;
      border: 2px solid #1c5980;
      border-radius: 8px;
      padding: 6px 12px;
      cursor: pointer;
      min-width: 120px;
      transition: border-color 0.3s ease;
    }
    .lang-select:focus {
      outline: none;
      border-color: #8fc1a1;
      box-shadow: 0 0 5px #8fc1a1;
    }
    .hero {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-around;
      padding: 4rem 2rem;
      background: linear-gradient(to right, #1c5980, #8fc1a1);
      color: white;
      flex-shrink: 0;
    }
    .hero-text {
      max-width: 500px;
      flex: 1 1 300px;
    }
    .hero-text h1 {
      margin-top: 0;
      font-weight: 700;
      font-size: 2.5rem;
      line-height: 1.1;
    }
    .hero-text p {
      font-weight: 300;
      font-size: 1.2rem;
      margin-top: 0.8rem;
    }
    .hero img {
      max-width: 400px;
      width: 100%;
      border-radius: 12px;
      margin-top: 2rem;
      flex: 1 1 350px;
      user-select: none;
    }
    main {
      flex-grow: 1;
      max-width: 900px;
      margin: 0 auto 2rem auto;
      padding: 0 1rem;
      width: 100%;
    }
    section {
      margin-bottom: 3rem;
    }
    h2 {
      color: #1c5980;
      font-weight: 700;
      margin-bottom: 1rem;
      font-size: 1.8rem;
    }
    p {
      font-weight: 400;
      font-size: 1.1rem;
      margin-top: 0;
      color: #204d7a;
    }
    .stats {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 2rem;
    }
    .stat {
      background: white;
      border-left: 6px solid #8fc1a1;
      padding: 1.5rem;
      border-radius: 12px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      color: #1c5980;
      user-select: none;
    }
    .stat strong {
      display: block;
      font-size: 1.4rem;
      margin-bottom: 0.5rem;
    }
    .faq details {
      margin-bottom: 1rem;
      background: white;
      padding: 1rem;
      border-radius: 8px;
      cursor: pointer;
      box-shadow: 0 2px 6px rgb(0 0 0 / 0.05);
      color: #1c5980;
    }
    .faq summary {
      font-weight: 600;
      font-size: 1.1rem;
      outline: none;
    }
    .faq p {
      margin: 0.5rem 0 0 1rem;
      font-weight: 400;
      font-size: 1rem;
      color: #35648f;
    }
    .contact-form {
      background: white;
      padding: 2rem;
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      max-width: 500px;
      margin: auto;
      color: #1c5980;
    }
    .contact-form label {
      display: block;
      margin-bottom: 0.5rem;
      font-weight: 600;
    }
    .contact-form input,
    .contact-form textarea {
      width: 100%;
      padding: 8px 10px;
      margin-bottom: 1rem;
      border: 1.5px solid #ccc;
      border-radius: 6px;
      font-size: 1rem;
      font-family: 'Poppins', sans-serif;
      box-sizing: border-box;
      resize: vertical;
      transition: border-color 0.3s ease;
    }
    .contact-form input:focus,
    .contact-form textarea:focus {
      border-color: #8fc1a1;
      outline: none;
      box-shadow: 0 0 5px #8fc1a1;
    }
    .contact-form button {
      background-color: #1c5980;
      color: white;
      border: none;
      padding: 12px 20px;
      font-size: 1rem;
      border-radius: 8px;
      cursor: pointer;
      font-weight: 700;
      transition: background-color 0.3s ease;
    }
    .contact-form button:hover {
      background-color: #8fc1a1;
      color: #1c5980;
    }
    footer {
      text-align: center;
      padding: 1rem;
      background: #1c5980;
      color: white;
      font-size: 0.9rem;
      flex-shrink: 0;
      user-select: none;
    }
    footer a {
      color: #8fc1a1;
      text-decoration: underline;
    }
    @media (max-width: 768px) {
      .hero {
        flex-direction: column;
        text-align: center;
      }
      .hero img {
        margin-top: 1.5rem;
      }
    }
    .carousel {
      max-width: 900px;
      margin: 3rem auto;
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
    }
    .carousel-slide {
      min-width: 100%;
    }
    .carousel-slide img {
      width: 100%;
      height: auto;
      display: block;
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
      font-size: 2rem;
      padding: 0.3rem 0.8rem;
      cursor: pointer;
      border-radius: 50%;
      transition: background-color 0.3s ease;
      user-select: none;
      z-index: 10;
    }
    .carousel-button:hover {
      background: #8fc1a1cc;
      color: #1c5980;
    }
    .carousel-button.prev {
      left: 10px;
    }
    .carousel-button.next {
      right: 10px;
    }
    #whitepaper {
      background: white;
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      padding: 3rem 2rem;
      max-width: 900px;
      margin: 3rem auto;
      text-align: center;
      color: #1c5980;
      user-select: none;
    }
    #whitepaper h2 {
      margin-bottom: 1rem;
    }
    #whitepaper p {
      max-width: 700px;
      margin: 0 auto 2rem;
      color: #204d7a;
      font-size: 1.1rem;
    }
    #whitepaper a {
      display: inline-block;
      padding: 12px 28px;
      background-color: #1c5980;
      color: white;
      font-weight: 700;
      font-family: 'Poppins', sans-serif;
      border-radius: 8px;
      text-decoration: none;
      transition: background-color 0.3s ease;
    }
    #whitepaper a:hover {
      background-color: #8fc1a1;
      color: #1c5980;
    }
  </style>
</head>
<body>
  <header>
    <strong>Silent Witness</strong>
    <div>
      <label for="lang" class="visually-hidden">Choisir la langue</label>
      <select id="lang" class="lang-select" onchange="switchLang()" aria-label="Choisir la langue">
        <option value="fr" selected>🇫🇷 Français</option>
        <option value="en">🇬🇧 English</option>
      </select>
    </div>
  </header>

  <div class="hero">
    <div class="hero-text">
      <h1 id="hero-title"></h1>
      <p id="hero-desc"></p>
    </div>
    <img
      src="https://raw.githubusercontent.com/silentwitnessteam/silentwitness/main/illustration.png"
      alt="Illustration IA et humain"
      loading="lazy"
    />
  </div>

  <main>
    <section id="concept" tabindex="0" aria-label="Notre mission">
      <h2 id="mission-title"></h2>
      <p id="mission-desc"></p>
    </section>

    <section id="stats" tabindex="0" aria-label="Statistiques clés">
      <h2 id="stats-title"></h2>
      <div class="stats">
        <div class="stat">
          <strong id="stat1"></strong>
          <p id="stat1-desc"></p>
        </div>
        <div class="stat">
          <strong id="stat2"></strong>
          <p id="stat2-desc"></p>
        </div>
        <div class="stat">
          <strong id="stat3"></strong>
          <p id="stat3-desc"></p>
        </div>
      </div>
    </section>

    <section id="whitepaper" tabindex="0" aria-label="White Paper Silent Witness">
      <h2 id="whitepaper-title"></h2>
      <p id="whitepaper-desc"></p>
      <!-- Ici on retire le lien PDF externe puisque tu ne veux pas de fichiers -->
    </section>

    <section id="faq" class="faq" tabindex="0" aria-label="Foire aux questions">
      <h2>FAQ</h2>
      <details>
        <summary id="faq1"></summary>
        <p id="faq1-desc"></p>
      </details>
      <details>
        <summary id="faq2"></summary>
        <p id="faq2-desc"></p>
      </details>
      <details>
        <summary id="faq3"></summary>
        <p id="faq3-desc"></p>
      </details>
      <details>
        <summary id="faq4"></summary>
        <p id="faq4-desc"></p>
      </details>
    </section>

    <section id="visuals" tabindex="0" aria-label="Galerie images humain et technologie">
      <h2 id="visuals-title"></h2>
      <div class="carousel" aria-live="polite">
        <button class="carousel-button prev" aria-label="Image précédente">&#10094;</button>
        <div class="carousel-track">
          <div class="carousel-slide">
            <img src="https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=800&q=80" alt="Homme avec un casque de réalité augmentée" loading="lazy" />
          </div>
          <div class="carousel-slide">
            <img src="https://images.unsplash.com/photo-1497493292307-31c376b6e479?auto=format&fit=crop&w=800&q=80" alt="Femme et robot collaborant ensemble" loading="lazy" />
          </div>
          <div class="carousel-slide">
            <img src="https://images.unsplash.com/photo-1518770660439-4636190af475?auto=format&fit=crop&w=800&q=80" alt="Visage humain et visage robot en transparence" loading="lazy" />
          </div>
        </div>
        <button class="carousel-button next" aria-label="Image suivante">&#10095;</button>
      </div>
    </section>

    <section id="contact" tabindex="0" aria-label="Formulaire de contact">
      <h2 id="contact-title"></h2>
      <form
        class="contact-form"
        action="mailto:silentwitness@outlook.fr"
        method="post"
        enctype="text/plain"
      >
        <label for="nom" id="label-nom"></label>
        <input type="text" name="nom" id="nom" required autocomplete="name" />

        <label for="email" id="label-email"></label>
        <input type="email" name="email" id="email" required autocomplete="email" />

        <label for="message" id="label-message"></label>
        <textarea name="message" id="message" rows="5" required></textarea>

        <button type="submit" id="btn-send"></button>
      </form>
    </section>
  </main>

  <footer>
    © 2025 Silent Witness — IA pour la prévention, l'éthique et la vie.
  </footer>

  <script>
    const translations = {
      fr: {
        "hero-title": "L'IA au service de l'humain",
        "hero-desc": "Détection éthique des signaux de détresse, pour sauver des vies en toute confidentialité.",
        "mission-title": "Notre mission",
        "mission-desc": "Silent Witness est une solution d’intelligence artificielle capable de détecter les signaux de détresse dans la voix, les gestes ou les recherches d’un individu. Elle classe ces signaux par gravité, puis transmet une alerte éthique et sécurisée aux secours appropriés : ONG, hôpitaux, ou autorités compétentes.",
        "stats-title": "Statistiques Clés",
        "stat1": "1 suicide toutes les 40 secondes",
        "stat1-desc": "dans le monde entier",
        "stat2": "+30%",
        "stat2-desc": "de chances d'intervention si le danger est détecté tôt",
        "stat3": "95%",
        "stat3-desc": "des utilisateurs croient au potentiel éthique de l'IA",
        "whitepaper-title": "White Paper",
        "whitepaper-desc": "Découvrez en détail notre démarche, la technologie, l’éthique et la vision derrière Silent Witness. Ce document présente les objectifs, la technologie utilisée, et l’impact social de notre IA au service de l’humain.",
        "faq1": "L’IA accède-t-elle à des données privées ?",
        "faq1-desc": "Non. Silent Witness n'enregistre aucune donnée personnelle...",
        "faq2": "Comment les alertes sont-elles transmises ?",
        "faq2-desc": "Via une base de données sécurisée et cryptée...",
        "faq3": "Est-ce déjà en service ?",
        "faq3-desc": "Silent Witness est en phase de prototypage avancé...",
        "faq4": "Qui peut nous contacter ?",
        "faq4-desc": "ONG, hôpitaux, développeurs IA, chercheurs...",
        "contact-title": "Contact",
        "visuals-title": "Humain & Technologie",
        "label-nom": "Nom:",
        "label-email": "Email:",
        "label-message": "Message:",
        "btn-send": "Envoyer"
      },
      en: {
        "hero-title": "AI serving humanity",
        "hero-desc": "Ethical detection of distress signals to save lives confidentially.",
        "mission-title": "Our Mission",
        "mission-desc": "Silent Witness is an AI solution that detects distress signals in voice, gestures or online searches. It classifies them by severity, then sends an ethical and secure alert to appropriate responders: NGOs, hospitals, or authorities.",
        "stats-title": "Key Statistics",
        "stat1": "1 suicide every 40 seconds",
        "stat1-desc": "worldwide",
        "stat2": "+30%",
        "stat2-desc": "increase in intervention chances if danger is detected early",
        "stat3": "95%",
        "stat3-desc": "users believe in AI’s ethical potential",
        "whitepaper-title": "White Paper",
        "whitepaper-desc": "Discover in detail our approach, technology, ethics, and vision behind Silent Witness. This document presents objectives, technologies used, and the social impact of our AI serving humanity.",
        "faq1": "Does the AI access private data?",
        "faq1-desc": "No. Silent Witness does not record any personal data...",
        "faq2": "How are alerts transmitted?",
        "faq2-desc": "Via a secure and encrypted database...",
        "faq3": "Is it already operational?",
        "faq3-desc": "Silent Witness is currently in advanced prototyping...",
        "faq4": "Who can contact us?",
        "faq4-desc": "NGOs, hospitals, AI developers, researchers...",
        "contact-title": "Contact",
        "visuals-title": "Human & Technology",
        "label-nom": "Name:",
        "label-email": "Email:",
        "label-message": "Message:",
        "btn-send": "Send"
      }
    };

    function switchLang() {
      const lang = document.getElementById('lang').value;
      document.documentElement.lang = lang;
      document.documentElement.dir = lang === 'en' ? 'ltr' : 'ltr'; // both left-to-right here

      const keys = Object.keys(translations.fr);

      keys.forEach(id => {
        const el = document.getElementById(id);
        if (!el) return;
        el.textContent = translations[lang][id] || el.textContent;
      });

      // Also update form labels and button values
      document.getElementById('nom').placeholder = translations[lang]['label-nom'];
      document.getElementById('email').placeholder = translations[lang]['label-email'];
      document.getElementById('message').placeholder = translations[lang]['label-message'];
    }

    document.addEventListener('DOMContentLoaded', () => {
      switchLang();

      // Carousel
      const track = document.querySelector('.carousel-track');
      const slides = Array.from(track.children);
      const prevBtn = document.querySelector('.carousel-button.prev');
      const nextBtn = document.querySelector('.carousel-button.next');
      let currentIndex = 0;

      function updateCarousel() {
        const slideWidth = slides[0].getBoundingClientRect().width;
        track.style.transform = `translateX(-${slideWidth * currentIndex}px)`;
      }

      prevBtn.addEventListener('click', () => {
        currentIndex = (currentIndex - 1 + slides.length) % slides.length;
        updateCarousel();
      });

      nextBtn.addEventListener('click', () => {
        currentIndex = (currentIndex + 1) % slides.length;
        updateCarousel();
      });

      window.addEventListener('resize', updateCarousel);
      updateCarousel();
    });
  </script>
</body>
</html>

