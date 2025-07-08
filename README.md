<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Silent Witness - IA au service de l'humain</title>
  <link
    href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap"
    rel="stylesheet"
  />
  <!-- Favicon simple (œil stylisé) -->
  <link rel="icon" href="https://raw.githubusercontent.com/silentwitnessteam/silentwitness/main/favicon.svg" type="image/svg+xml" />
  <style>
    /* Reset & global */
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: #f5f7fa;
      color: #1c5980;
      line-height: 1.5;
    }

    /* Header */
    header {
      background-color: #1c5980;
      color: white;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
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
      min-width: 140px;
      max-width: 100%;
      box-sizing: border-box;
      transition: border-color 0.3s ease;
    }
    .lang-select:focus {
      outline: none;
      border-color: #8fc1a1;
      box-shadow: 0 0 5px #8fc1a1;
    }

    /* Hero */
    .hero {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-around;
      padding: 4rem 2rem;
      background: linear-gradient(to right, #1c5980, #8fc1a1);
      color: white;
    }
    .hero-text {
      max-width: 500px;
    }
    .hero img {
      max-width: 400px;
      width: 100%;
      border-radius: 12px;
      margin-top: 2rem;
    }

    /* Sections */
    section {
      padding: 3rem 2rem;
      max-width: 900px;
      margin: auto;
    }
    .stats {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 2rem;
      margin-top: 2rem;
    }
    .stat {
      background: white;
      border-left: 6px solid #8fc1a1;
      padding: 1.5rem;
      border-radius: 12px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    .faq details {
      margin-bottom: 1rem;
      background: white;
      padding: 1rem;
      border-radius: 8px;
      cursor: pointer;
    }

    /* Contact form */
    .contact-form {
      background: white;
      padding: 2rem;
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      max-width: 500px;
      margin: auto;
    }
    .contact-form label {
      display: block;
      margin-bottom: 0.5rem;
      font-weight: 600;
      color: #1c5980;
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

    /* Footer */
    footer {
      text-align: center;
      padding: 1rem;
      background: #1c5980;
      color: white;
      font-size: 0.9rem;
    }
    footer a {
      color: #8fc1a1;
      text-decoration: underline;
    }

    /* Responsive */
    @media (max-width: 768px) {
      .hero {
        flex-direction: column;
        text-align: center;
      }
      .hero img {
        margin-top: 1.5rem;
      }
    }

    /* Animations subtiles */
    .fade-in {
      animation: fadeInAnim 1.5s ease forwards;
      opacity: 0;
    }
    @keyframes fadeInAnim {
      to { opacity: 1; }
    }

    /* Carrousel images */
    .carousel {
      max-width: 900px;
      margin: 3rem auto;
      overflow: hidden;
      border-radius: 12px;
      box-shadow: 0 5px 15px rgba(28,89,128,0.3);
      background: white;
      position: relative;
    }
    .carousel-track {
      display: flex;
      transition: transform 0.5s ease;
    }
    .carousel-slide {
      min-width: 100%;
      user-select: none;
    }
    .carousel-slide img {
      width: 100%;
      height: auto;
      display: block;
      border-radius: 12px;
    }

    /* Carousel navigation buttons */
    .carousel-button {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      background: #1c5980cc;
      border: none;
      color: white;
      font-size: 1.8rem;
      padding: 0.3rem 0.8rem;
      cursor: pointer;
      border-radius: 50%;
      transition: background-color 0.3s ease;
      user-select: none;
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

    /* Retour en haut */
    #scrollTopBtn {
      display: none;
      position: fixed;
      bottom: 25px;
      right: 25px;
      background-color: #1c5980;
      color: white;
      border: none;
      padding: 0.6rem 1rem;
      border-radius: 8px;
      font-size: 1.2rem;
      cursor: pointer;
      box-shadow: 0 2px 6px rgba(28,89,128,0.7);
      transition: background-color 0.3s ease;
      z-index: 1000;
    }
    #scrollTopBtn:hover {
      background-color: #8fc1a1;
      color: #1c5980;
    }
  </style>
</head>
<body>
  <header>
    <div><strong>Silent Witness</strong></div>
    <div>
      <label for="lang" class="visually-hidden">Choisir la langue</label>
      <select id="lang" class="lang-select" onchange="switchLang()" aria-label="Choisir la langue">
        <option value="fr">🇫🇷 Français</option>
        <option value="en">🇬🇧 English</option>
        <option value="ar">🇸🇦 العربية</option>
      </select>
    </div>
  </header>

  <div class="hero">
    <div class="hero-text">
      <h1 id="hero-title">L'IA au service de l'humain</h1>
      <p id="hero-desc">Détection éthique des signaux de détresse, pour sauver des vies en toute confidentialité.</p>
    </div>
    <img src="https://raw.githubusercontent.com/silentwitnessteam/silentwitness/main/illustration.png" alt="Illustration IA et humain" />
  </div>

  <section id="concept">
    <h2 id="mission-title">Notre mission</h2>
    <p id="mission-desc">
      Silent Witness est une solution d’intelligence artificielle capable de détecter les signaux de détresse dans la voix, les gestes ou les recherches d’un individu. Elle classe ces signaux par gravité, puis transmet une alerte éthique et sécurisée aux secours appropriés : ONG, hôpitaux, ou autorités compétentes.
    </p>
  </section>

  <section id="stats">
    <h2 id="stats-title">Statistiques Clés</h2>
    <div class="stats">
      <div class="stat">
        <strong id="stat1">1 suicide toutes les 40 secondes</strong>
        <p id="stat1-desc">dans le monde entier</p>
      </div>
      <div class="stat">
        <strong id="stat2">+30%</strong>
        <p id="stat2-desc">de chances d'intervention si le danger est détecté tôt</p>
      </div>
      <div class="stat">
        <strong id="stat3">95%</strong>
        <p id="stat3-desc">des utilisateurs croient au potentiel éthique de l'IA</p>
      </div>
    </div>
  </section>

  <section id="faq" class="faq">
    <h2>FAQ</h2>
    <details>
      <summary id="faq1">L’IA accède-t-elle à des données privées ?</summary>
      <p id="faq1-desc">Non. Silent Witness n'enregistre aucune donnée personnelle...</p>
    </details>
    <details>
      <summary id="faq2">Comment les alertes sont-elles transmises ?</summary>
      <p id="faq2-desc">Via une base de données sécurisée et cryptée...</p>
    </details>
    <details>
      <summary id="faq3">Est-ce déjà en service ?</summary>
      <p id="faq3-desc">Silent Witness est en phase de prototypage avancé...</p>
    </details>
    <details>
      <summary id="faq4">Qui peut nous contacter ?</summary>
      <p id="faq4-desc">ONG, hôpitaux, développeurs IA, chercheurs...</p>
    </details>
  </section>

  <!-- Nouvelle section galerie d'images -->
  <section id="visuals">
    <h2>Humain & Technologie</h2>
    <div class="carousel fade-in" aria-label="Galerie d'images humains et IA">
      <button class="carousel-button prev" aria-label="Image précédente">&#10094;</button>
      <div class="carousel-track">
        <div class="carousel-slide">
          <img src="https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=800&q=80" alt="Homme avec un casque de réalité augmentée" />
        </div>
        <div class="carousel-slide">
          <img src="https://images.unsplash.com/photo-1497493292307-31c376b6e479?auto=format&fit=crop&w=800&q=80" alt="Femme et robot collaborant ensemble" />
        </div>
        <div class="carousel-slide">
          <img src="https://images.unsplash.com/photo-1518770660439-4636190af475?auto=format&fit=crop&w=800&q=80" alt="Visage humain et visage robot en transparence" />
        </div>
      </div>
      <button class="carousel-button next" aria-label="Image suivante">&#10095;</button>
    </div>
  </section>

  <section id="contact">
    <h2 id="contact-title">Contact</h2>
    <form
      class="contact-form"
      action="mailto:silentwitness@outlook.fr"
      method="post"
      enctype="text/plain"
    >
      <label for="nom">Nom:</label>
      <input type="text" name="nom" id="nom" required />

      <label for="email">Email:</label>
      <input type="email" name="email" id="email" required />

      <label for="message">Message:</label>
      <textarea name="message" id="message" rows="5" required></textarea>

      <button type="submit">Envoyer</button>
    </form>
  </section>

  <footer>
    © 2025 Silent Witness — IA pour la prévention, l'éthique et la vie.<br />
    <a href="SilentWitness_WhitePaper.pdf" target="_blank" rel="noopener">Télécharger notre White Paper</a>
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
        "faq1": "L’IA accède-t-elle à des données privées ?",
        "faq1-desc": "Non. Silent Witness n'enregistre aucune donnée personnelle...",
        "faq2": "Comment les alertes sont-elles transmises ?",
        "faq2-desc": "Via une base de données sécurisée et cryptée...",
        "faq3": "Est-ce déjà en service ?",
        "faq3-desc": "Silent Witness est en phase de prototypage avancé...",
        "faq4": "Qui peut nous contacter ?",
        "faq4-desc": "ONG, hôpitaux, développeurs IA, chercheurs...",
        "contact-title": "Contact"
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
        "stat2-desc
