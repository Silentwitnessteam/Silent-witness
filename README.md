<!DOCTYPE html>
<html lang="fr" dir="ltr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Silent Witness - IA au service de l'humain</title>
  <link
    href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap"
    rel="stylesheet"
  />
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
      line-height: 1.6;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 2rem 1rem;
    }
    main {
      max-width: 900px;
      width: 100%;
    }
    h1, h2 {
      margin-top: 0;
      font-weight: 700;
    }
    h1 {
      font-size: 2.8rem;
      margin-bottom: 0.5rem;
    }
    h2 {
      font-size: 2rem;
      margin-bottom: 1rem;
      color: #204d7a;
    }
    p {
      font-weight: 400;
      font-size: 1.15rem;
      color: #204d7a;
      margin-bottom: 2rem;
    }

    /* Header */
    header {
      background-color: #1c5980;
      color: white;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-shrink: 0;
      width: 100%;
      max-width: 900px;
      border-radius: 12px;
      box-sizing: border-box;
      user-select: none;
      margin-bottom: 2rem;
    }
    header strong {
      font-size: 1.5rem;
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
      transition: border-color 0.3s ease;
    }
    .lang-select:focus {
      outline: none;
      border-color: #8fc1a1;
      box-shadow: 0 0 5px #8fc1a1;
    }

    /* Barre de progression container */
    .progress-container {
      width: 100%;
      height: 40px;
      background: #ddd;
      border-radius: 20px;
      overflow: hidden;
      margin: 3rem 0 4rem 0;
      box-shadow: 0 3px 8px rgba(28,89,128,0.15);
      position: relative;
      user-select: none;
    }
    /* Barre de progression animée */
    .progress-bar {
      height: 100%;
      width: 75%; /* Ajuste la progression ici */
      background: linear-gradient(90deg, #1c5980, #8fc1a1);
      display: flex;
      justify-content: center;
      align-items: center;
      color: white;
      font-weight: 700;
      font-size: 1.3rem;
      position: relative;
      animation: fillProgress 2.5s ease forwards;
    }
    /* Texte animé dans la barre */
    .progress-text {
      animation: moveText 3.5s linear infinite;
      white-space: nowrap;
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
    }
    @keyframes fillProgress {
      0% {
        width: 0;
      }
      100% {
        width: 75%;
      }
    }
    @keyframes moveText {
      0%, 100% {
        transform: translateX(-50%);
      }
      50% {
        transform: translateX(calc(-50% + 15px));
      }
    }

    /* Carousel styles */
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

    /* FAQ */
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

    /* Contact form */
    .contact-form {
      background: white;
      padding: 2rem;
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      max-width: 500px;
      margin: 2rem auto 4rem auto;
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

    /* Footer */
    footer {
      text-align: center;
      padding: 1rem;
      background: #1c5980;
      color: white;
      font-size: 0.9rem;
      flex-shrink: 0;
      user-select: none;
      border-radius: 0 0 12px 12px;
      width: 100%;
      max-width: 900px;
      margin: 0 auto 1rem auto;
      box-sizing: border-box;
    }
    footer a {
      color: #8fc1a1;
      text-decoration: underline;
    }

    /* Responsive */
    @media (max-width: 768px) {
      h1 {
        font-size: 2rem;
      }
      h2 {
        font-size: 1.5rem;
      }
      .progress-bar {
        font-size: 1rem;
      }
      header {
        padding: 1rem;
        flex-direction: column;
        gap: 1rem;
        border-radius: 12px;
      }
    }
  </style>
</head>
<body>

  <header>
    <strong>Silent Witness</strong>
    <select id="lang" class="lang-select" aria-label="Choisir la langue" onchange="switchLang()">
      <option value="fr">🇫🇷 Français</option>
      <option value="en">🇬🇧 English</option>
      <option value="ar">🇸🇦 العربية</option>
    </select>
  </header>

  <main>
    <h1 id="hero-title">L'IA au service de l'humain</h1>
    <p id="hero-desc">
      Détection éthique des signaux de détresse, pour sauver des vies en toute confidentialité.
    </p>

    <div class="progress-container" role="progressbar" aria-valuemin="0" aria-valuemax="100" aria-valuenow="75" tabindex="0">
      <div class="progress-bar">
        <span class="progress-text" id="progress-text">You’re not alone — Vous n’êtes pas seul — لست وحدك</span>
      </div>
    </div>

    <section>
      <h2 id="mission-title">Notre mission</h2>
      <p id="mission-desc">
        Silent Witness est une solution d’intelligence artificielle capable de détecter les signaux de détresse dans la voix, les gestes ou les recherches d’un individu.
        Elle classe ces signaux par gravité, puis transmet une alerte éthique et sécurisée aux secours appropriés : ONG, hôpitaux, ou autorités compétentes.
      </p>
    </section>

    <section id="stats" tabindex="0" aria-label="Statistiques clés">
      <h2 id="stats-title">Statistiques Clés</h2>
      <p><strong id="stat1">1 suicide toutes les 40 secondes</strong> <span id="stat1-desc">dans le monde entier.</span></p>
      <p><strong id="stat2">+30%</strong> <span id="stat2-desc">de chances d'intervention si le danger est détecté tôt.</span></p>
      <p><strong id="stat3">95%</strong> <span id="stat3-desc">des utilisateurs croient au potentiel éthique de l'IA.</span></p>
    </section>

    <section class="carousel" aria-label="Galerie images humain et technologie" tabindex="0">
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
    </section>

    <section class="faq" tabindex="0" aria-label="Foire aux questions">
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

    <section id="contact" tabindex="0" aria-label="Formulaire de contact">
      <h2 id="contact-title">Contact</h2>
      <form
        class="contact-form"
        action="mailto:silentwitness@outlook.fr"
        method="post"
        enctype="text/plain"
      >
        <label for="nom">Nom:</label>
        <input type="text" name="nom" id="nom" required autocomplete="name" />

        <label for="email">Email:</label>
        <input type="email" name="email" id="email" required autocomplete="email" />

        <label for="message">Message:</label>
        <textarea name="message" id="message" rows="5" required></textarea>

        <button type="submit">Envoyer</button>
      </form>
    </section>
  </main>

  <footer>
    © 2025 Silent Witness — IA pour la prévention, l'éthique et la vie.
  </footer>

  <script>
    // Texte multilingue
    const translations = {
      fr: {
        "hero-title": "L'IA au service de l'humain",
        "hero-desc": "Détection éthique des signaux de détresse, pour sauver des vies en toute confidentialité.",
        "mission-title": "Notre mission",
        "mission-desc": "Silent Witness est une solution d’intelligence artificielle capable de détecter les signaux de détresse dans la voix, les gestes ou les recherches d’un individu. Elle classe ces signaux par gravité, puis transmet une alerte éthique et sécurisée aux secours appropriés : ONG, hôpitaux, ou autorités compétentes.",
        "stats-title": "Statistiques Clés",
        "stat1": "1 suicide toutes les 40 secondes",
        "stat1-desc": "dans le monde entier.",
        "stat2": "+30%",
        "stat2-desc": "de chances d'intervention si le danger est détecté tôt.",
        "stat3": "95%",
        "stat3-desc": "des utilisateurs croient au potentiel éthique de l'IA.",
        "faq1": "L’IA accède-t-elle à des données privées ?",
        "faq1-desc": "Non. Silent Witness n'enregistre aucune donnée personnelle...",
        "faq2": "Comment les alertes sont-elles transmises ?",
        "faq2-desc": "Via une base de données sécurisée et cryptée...",
        "faq3": "Est-ce déjà en service ?",
        "faq3-desc": "Silent Witness est en phase de prototypage avancé...",
        "faq4": "Qui peut nous contacter ?",
        "faq4-desc": "ONG, hôpitaux, développeurs IA, chercheurs...",
        "contact-title": "Contact",
        "progress-text": "Vous n’êtes pas seul — You’re not alone — لست وحدك",
        "contact-nom": "Nom:",
        "contact-email": "Email:",
        "contact-message": "Message:",
        "contact-send": "Envoyer"
      },
      en: {
        "hero-title": "AI serving humanity",
        "hero-desc": "Ethical detection of distress signals to save lives confidentially.",
        "mission-title": "Our Mission",
        "mission-desc": "Silent Witness is an AI solution that detects distress signals in voice, gestures or online searches. It classifies them by severity, then sends an ethical and secure alert to appropriate responders: NGOs, hospitals, or authorities.",
        "stats-title": "Key Statistics",
        "stat1": "1 suicide every 40 seconds",
        "stat1-desc": "worldwide.",
        "stat2": "+30%",
        "stat2-desc": "increase in intervention chances if danger is detected early.",
        "stat3": "95%",
        "stat3-desc": "users believe in AI’s ethical potential.",
        "faq1": "Does the AI access private data?",
        "faq1-desc": "No. Silent Witness does not record any personal data...",
        "faq2": "How are alerts transmitted?",
        "faq2-desc": "Via a secure and encrypted database...",
        "faq3": "Is it already operational?",
        "faq3-desc": "Silent Witness is currently in advanced prototyping...",
        "faq4": "Who can contact us?",
        "faq4-desc": "NGOs, hospitals, AI developers, researchers...",
        "contact-title": "Contact",
        "progress-text": "You’re not alone — Vous n’êtes pas seul — لست وحدك",
        "contact-nom": "Name:",
        "contact-email": "Email:",
        "contact-message": "Message:",
        "contact-send": "Send"
      },
      ar: {
        "hero-title": "الذكاء الاصطناعي في خدمة الإنسانية",
        "hero-desc": "الكشف الأخلاقي عن إشارات الضيق لإنقاذ الأرواح بسرية تامة.",
        "mission-title": "مهمتنا",
        "mission-desc": "Silent Witness هو حل ذكاء اصطناعي يكتشف إشارات الضيق في الصوت، والإيماءات، أو عمليات البحث على الإنترنت. يصنف هذه الإشارات حسب شدتها، ثم يرسل تنبيهًا أخلاقيًا وآمنًا للمستجيبين المناسبين: منظمات غير حكومية، مستشفيات، أو السلطات المختصة.",
        "stats-title": "إحصائيات رئيسية",
        "stat1": "انتحار واحد كل 40 ثانية",
        "stat1-desc": "في جميع أنحاء العالم.",
        "stat2": "+30%",
        "stat2-desc": "زيادة في فرص التدخل إذا تم اكتشاف الخطر مبكرًا.",
        "stat3": "95%",
        "stat3-desc": "من المستخدمين يؤمنون بالإمكانات الأخلاقية للذكاء الاصطناعي.",
        "faq1": "هل يصل الذكاء الاصطناعي إلى بيانات خاصة؟",
        "faq1-desc": "لا. Silent Witness لا يسجل أية بيانات شخصية...",
        "faq2": "كيف تُنقل التنبيهات؟",
        "faq2-desc": "عبر قاعدة بيانات مؤمنة ومشفرة...",
        "faq3": "هل هو قيد الخدمة بالفعل؟",
        "faq3-desc": "Silent Witness في مرحلة النماذج الأولية المتقدمة...",
        "faq4": "من يمكنه التواصل معنا؟",
        "faq4-desc": "المنظمات غير الحكومية، المستشفيات، مطورو الذكاء الاصطناعي، الباحثون...",
        "contact-title": "اتصل بنا",
        "progress-text": "لست وحدك — You’re not alone — Vous n’êtes pas seul",
        "contact-nom": "الاسم:",
        "contact-email": "البريد الإلكتروني:",
        "contact-message": "الرسالة:",
        "contact-send": "إرسال"
      }
    };

    // Fonction pour changer la langue
    function switchLang() {
      const lang = document.getElementById('lang').value;
      const texts = translations[lang];

      // Textes principaux
      document.getElementById('hero-title').textContent = texts["hero-title"];
      document.getElementById('hero-desc').textContent = texts["hero-desc"];
      document.getElementById('mission-title').textContent = texts["mission-title"];
      document.getElementById('mission-desc').textContent = texts["mission-desc"];
      document.getElementById('stats-title').textContent = texts["stats-title"];
      document.getElementById('stat1').textContent = texts["stat1"];
      document.getElementById('stat1-desc').textContent = texts["stat1-desc"];
      document.getElementById('stat2').textContent = texts["stat2"];
      document.getElementById('stat2-desc').textContent = texts["stat2-desc"];
      document.getElementById('stat3').textContent = texts["stat3"];
      document.getElementById('stat3-desc').textContent = texts["stat3-desc"];
      document.getElementById('faq1').textContent = texts["faq1"];
      document.getElementById('faq1-desc').textContent = texts["faq1-desc"];
      document.getElementById('faq2').textContent = texts["faq2"];
      document.getElementById('faq2-desc').textContent = texts["faq2-desc"];
      document.getElementById('faq3').textContent = texts["faq3"];
      document.getElementById('faq3-desc').textContent = texts["faq3-desc"];
      document.getElementById('faq4').textContent = texts["faq4"];
      document.getElementById('faq4-desc').textContent = texts["faq4-desc"];
      document.getElementById('contact-title').textContent = texts["contact-title"];

      // Contact form labels & button
      document.querySelector('label[for="nom"]').textContent = texts["contact-nom"];
      document.querySelector('label[for="email"]').textContent = texts["contact-email"];
      document.querySelector('label[for="message"]').textContent = texts["contact-message"];
      document.querySelector('.contact-form button').textContent = texts["contact-send"];

      // Barre progression texte
      document.getElementById('progress-text').textContent = texts["progress-text"];

      // Direction de page pour l'arabe
      if (lang === 'ar') {
        document.documentElement.setAttribute('dir', 'rtl');
        document.body.style.textAlign = 'right';
      } else {
        document.documentElement.setAttribute('dir', 'ltr');
        document.body.style.textAlign = 'left';
      }
    }

    // Initialisation à la langue par défaut
    switchLang();

    // Carrousel JS
    const track = document.querySelector('.carousel-track');
    const slides = Array.from(track.children);
    const nextBtn = document.querySelector('.carousel-button.next');
    const prevBtn = document.querySelector('.carousel-button.prev');
    let currentIndex = 0;

    function updateCarousel() {
      const slideWidth = slides[0].getBoundingClientRect().width;
      track.style.transform = `translateX(-${slideWidth * currentIndex}px)`;
    }

    nextBtn.addEventListener('click', () => {
      currentIndex = (currentIndex + 1) % slides.length;
      updateCarousel();
    });

    prevBtn.addEventListener('click', () => {
      currentIndex = (currentIndex - 1 + slides.length) % slides.length;
      updateCarousel();
    });

    // Resize listener to adjust carousel on window resize
    window.addEventListener('resize', updateCarousel);

    // Init carousel position
    updateCarousel();
  </script>

</body>
</html>
