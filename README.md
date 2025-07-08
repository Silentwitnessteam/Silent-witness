<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Silent Witness – IA au service de l'humain</title>
<style>
  /* === FONT & RESET === */
  @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&family=Poppins:wght@400;700&display=swap');

  * {
    box-sizing: border-box;
  }
  body {
    margin: 0; font-family: 'Poppins', 'Cairo', sans-serif;
    background: #fff; color: #222;
    transition: background 0.3s ease, color 0.3s ease;
  }
  body[data-theme='dark'] {
    background: #121212;
    color: #e0e0e0;
  }
  a {
    color: #1a73e8; text-decoration: none;
  }
  a:hover {
    text-decoration: underline;
  }

  /* === HEADER === */
  header {
    display: flex; justify-content: space-between; align-items: center;
    padding: 1rem 2rem;
    background: #004d7a;
    color: white;
  }
  body[data-theme='dark'] header {
    background: #00314a;
  }
  header strong {
    font-size: 1.5rem;
    user-select: none;
  }
  header > div {
    display: flex; align-items: center; gap: 1rem;
  }
  select.lang-select {
    font-size: 1rem;
    padding: 0.25rem 0.5rem;
    border-radius: 4px;
    border: none;
    cursor: pointer;
    font-family: 'Poppins', sans-serif;
  }
  button#theme-toggle {
    font-size: 1.5rem;
    background: transparent;
    border: none;
    cursor: pointer;
    color: inherit;
    user-select: none;
  }

  /* === HERO SECTION === */
  .hero {
    display: flex; flex-wrap: wrap; justify-content: center; align-items: center;
    padding: 2rem;
    gap: 2rem;
    background: #e8f1f8;
  }
  body[data-theme='dark'] .hero {
    background: #1a2633;
  }
  .hero-text {
    flex: 1 1 320px;
    max-width: 600px;
  }
  .hero-text h1 {
    font-size: 2.5rem;
    margin-bottom: 0.5rem;
  }
  .hero-text p {
    font-size: 1.25rem;
    margin-bottom: 1rem;
    line-height: 1.4;
  }
  .animated-text {
    font-size: 1.5rem;
    font-weight: 700;
    color: #004d7a;
    position: relative;
    overflow: hidden;
    white-space: nowrap;
  }
  body[data-theme='dark'] .animated-text {
    color: #7ec8e3;
  }
  /* Animation "typing" */
  .animated-text::after {
    content: '|';
    position: absolute;
    right: 0;
    animation: blink 1s steps(1) infinite;
  }
  @keyframes blink {
    0%, 50% { opacity: 1; }
    51%, 100% { opacity: 0; }
  }
  /* Carousel image */
  .hero img {
    flex: 1 1 320px;
    max-width: 400px;
    border-radius: 10px;
    object-fit: cover;
    box-shadow: 0 0 10px rgba(0,0,0,0.2);
  }

  /* === MAIN SECTIONS === */
  main {
    padding: 2rem;
    max-width: 1000px;
    margin: 0 auto;
  }
  section {
    margin-bottom: 3rem;
  }
  section h2 {
    font-size: 2rem;
    margin-bottom: 1rem;
    color: #004d7a;
  }
  body[data-theme='dark'] section h2 {
    color: #7ec8e3;
  }
  p {
    font-size: 1.1rem;
    line-height: 1.5;
  }

  /* === STATISTICS === */
  #stats .stats {
    display: flex; flex-wrap: wrap; gap: 1rem; justify-content: space-around;
  }
  .stat {
    background: #cde6f7;
    border-radius: 8px;
    padding: 1rem 1.5rem;
    flex: 1 1 280px;
    box-shadow: 1px 1px 5px rgba(0,0,0,0.1);
    color: #004d7a;
    text-align: center;
  }
  body[data-theme='dark'] #stats .stat {
    background: #23415a;
    color: #a7d0f4;
    box-shadow: none;
  }
  .stat strong {
    font-size: 1.5rem;
    display: block;
    margin-bottom: 0.25rem;
  }

  /* === CAROUSEL === */
  #visuals {
    text-align: center;
  }
  .carousel {
    position: relative;
    max-width: 800px;
    margin: 0 auto;
    overflow: hidden;
    border-radius: 10px;
  }
  .carousel-track {
    display: flex;
    transition: transform 0.5s ease-in-out;
  }
  .carousel-slide {
    min-width: 100%;
    user-select: none;
  }
  .carousel-slide img {
    width: 100%;
    display: block;
  }
  .carousel-button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: rgba(0,0,0,0.3);
    border: none;
    color: white;
    font-size: 2rem;
    cursor: pointer;
    padding: 0 10px;
    border-radius: 5px;
    user-select: none;
  }
  .carousel-button:hover {
    background: rgba(0,0,0,0.6);
  }
  .carousel-button.prev {
    left: 10px;
  }
  .carousel-button.next {
    right: 10px;
  }

  /* === FAQ === */
  .faq details {
    margin-bottom: 1rem;
    border: 1px solid #004d7a;
    border-radius: 6px;
    padding: 0.5rem 1rem;
    background: #f0f8ff;
  }
  body[data-theme='dark'] .faq details {
    background: #23415a;
    border-color: #7ec8e3;
  }
  .faq summary {
    cursor: pointer;
    font-weight: 700;
    font-size: 1.1rem;
    outline-offset: 4px;
  }
  .faq p {
    margin-top: 0.5rem;
  }

  /* === BUTTONS === */
  .btn {
    display: inline-block;
    background-color: #004d7a;
    color: white;
    padding: 0.6rem 1.2rem;
    border-radius: 6px;
    font-weight: 700;
    cursor: pointer;
    transition: background-color 0.3s ease;
    user-select: none;
    text-decoration: none;
  }
  .btn:hover {
    background-color: #00314a;
  }
  body[data-theme='dark'] .btn {
    background-color: #7ec8e3;
    color: #012f4a;
  }
  body[data-theme='dark'] .btn:hover {
    background-color: #56b0e6;
  }

  /* === CONTACT FORM === */
  #contact form {
    max-width: 600px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  label {
    font-weight: 600;
  }
  input[type="text"], input[type="email"], textarea {
    padding: 0.5rem;
    border-radius: 5px;
    border: 1px solid #ccc;
    font-family: inherit;
    font-size: 1rem;
    resize: vertical;
    transition: border-color 0.3s ease;
  }
  input[type="text"]:focus, input[type="email"]:focus, textarea:focus {
    outline: none;
    border-color: #004d7a;
  }
  body[data-theme='dark'] input[type="text"],
  body[data-theme='dark'] input[type="email"],
  body[data-theme='dark'] textarea {
    background: #23415a;
    border-color: #7ec8e3;
    color: #e0e0e0;
  }
  button[type="submit"] {
    width: 120px;
    padding: 0.5rem 1rem;
    font-weight: 700;
    font-size: 1.1rem;
    background: #004d7a;
    color: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    user-select: none;
    align-self: flex-start;
    transition: background-color 0.3s ease;
  }
  button[type="submit"]:hover {
    background: #00314a;
  }
  body[data-theme='dark'] button[type="submit"] {
    background: #7ec8e3;
    color: #012f4a;
  }
  body[data-theme='dark'] button[type="submit"]:hover {
    background: #56b0e6;
  }

  /* === FOOTER === */
  footer {
    text-align: center;
    padding: 1.5rem 1rem;
    font-size: 0.9rem;
    color: #666;
    user-select: none;
  }
  body[data-theme='dark'] footer {
    color: #aaa;
  }

  /* RESPONSIVE */
  @media (max-width: 700px) {
    .hero {
      flex-direction: column;
      text-align: center;
    }
    .hero img {
      max-width: 90vw;
      margin: 0 auto;
    }
    #stats .stats {
      flex-direction: column;
      align-items: center;
    }
  }
</style>
</head>
<body data-theme="light">

<header>
  <strong>Silent Witness</strong>
  <div>
    <select id="lang-select" class="lang-select" aria-label="Choix de la langue">
      <option value="fr">🇫🇷 Français</option>
      <option value="en">🇬🇧 English</option>
      <option value="ar">🇸🇦 العربية</option>
    </select>
    <button id="theme-toggle" aria-label="Changer le thème">🌓</button>
  </div>
</header>

<section class="hero">
  <div class="hero-text">
    <h1 id="hero-title">L'IA au service de l'humain</h1>
    <p id="hero-desc">Détection éthique des signaux de détresse, pour sauver des vies en toute confidentialité.</p>
    <div class="animated-text" aria-label="Texte animé">You're not alone</div>
  </div>
  <img src="https://images.unsplash.com/photo-1682687220125-5d08c9e75dc4?auto=format&fit=crop&w=800&q=80" alt="IA et humain" />
</section>

<main>
  <section id="mission">
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

  <section id="visuals">
    <h2>Humain & Technologie</h2>
    <div class="carousel">
      <button class="carousel-button prev" aria-label="Image précédente">&#10094;</button>
      <div class="carousel-track">
        <div class="carousel-slide">
          <img src="https://images.unsplash.com/photo-1617791160536-f74a90d52db5?auto=format&fit=crop&w=800&q=80" alt="Visage IA flouté" />
        </div>
        <div class="carousel-slide">
          <img src="https://images.unsplash.com/photo-1603988363603-6c4b0a6b9e33?auto=format&fit=crop&w=800&q=80" alt="Main humaine et main robot" />
        </div>
        <div class="carousel-slide">
          <img src="https://images.unsplash.com/photo-1605077081458-414d994db0d6?auto=format&fit=crop&w=800&q=80" alt="Humain assis avec écran d'IA" />
        </div>
      </div>
      <button class="carousel-button next" aria-label="Image suivante">&#10095;</button>
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

  <section id="whitepaper">
    <h2>Télécharger le White Paper</h2>
    <a href="Silent_Witness_White_Paper.pdf" download class="btn" aria-label="Télécharger le White Paper en PDF">📄 Télécharger (PDF)</a>
  </section>

  <section id="contact">
    <h2 id="contact-title">Contact</h2>
    <form class="contact-form" id="contact-form" aria-label="Formulaire de contact">
      <label for="name">Nom :</label>
      <input type="text" id="name" name="name" required autocomplete="name" />

      <label for="email">Email :</label>
      <input type="email" id="email" name="email" required autocomplete="email" />

      <label for="message">Message :</label>
      <textarea id="message" name="message" rows="4" required></textarea>

      <button type="submit">Envoyer</button>
    </form>
  </section>
</main>

<footer>
  <p>© 2025 Silent Witness — IA pour la prévention, l'éthique et la vie.</p>
</footer>

<script>
  // ==== THEME TOGGLE ====
  const themeToggleBtn = document.getElementById('theme-toggle');
  const bodyEl = document.body;

  themeToggleBtn.addEventListener('click', () => {
    if (bodyEl.getAttribute('data-theme') === 'light') {
      bodyEl.setAttribute('data-theme', 'dark');
      localStorage.setItem('theme', 'dark');
    } else {
      bodyEl.setAttribute('data-theme', 'light');
      localStorage.setItem('theme', 'light');
    }
  });

  // Apply saved theme on load
  const savedTheme = localStorage.getItem('theme');
  if(savedTheme) {
    bodyEl.setAttribute('data-theme', savedTheme);
  }

  // ==== LANGUAGE SWITCH ====
  const langSelect = document.getElementById('lang-select');

  // Text content for each language
  const translations = {
    fr: {
      'hero-title': "L'IA au service de l'humain",
      'hero-desc': "Détection éthique des signaux de détresse, pour sauver des vies en toute confidentialité.",
      'mission-title': "Notre mission",
      'mission-desc': "Silent Witness est une solution d’intelligence artificielle capable de détecter les signaux de détresse dans la voix, les gestes ou les recherches d’un individu. Elle classe ces signaux par gravité, puis transmet une alerte éthique et sécurisée aux secours appropriés : ONG, hôpitaux, ou autorités compétentes.",
      'stats-title': "Statistiques Clés",
      'stat1': "1 suicide toutes les 40 secondes",
      'stat1-desc': "dans le monde entier",
      'stat2': "+30%",
      'stat2-desc': "de chances d'intervention si le danger est détecté tôt",
      'stat3': "95%",
      'stat3-desc': "des utilisateurs croient au potentiel éthique de l'IA",
      'contact-title': "Contact",
      'faq1': "L’IA accède-t-elle à des données privées ?",
      'faq1-desc': "Non. Silent Witness n'enregistre aucune donnée personnelle...",
      'faq2': "Comment les alertes sont-elles transmises ?",
      'faq2-desc': "Via une base de données sécurisée et cryptée...",
      'faq3': "Est-ce déjà en service ?",
      'faq3-desc': "Silent Witness est en phase de prototypage avancé...",
      'faq4': "Qui peut nous contacter ?",
      'faq4-desc': "ONG, hôpitaux, développeurs IA, chercheurs...",
    },
    en: {
      'hero-title': "AI Serving Humanity",
      'hero-desc': "Ethical detection of distress signals to save lives confidentially.",
      'mission-title': "Our Mission",
      'mission-desc': "Silent Witness is an AI solution capable of detecting distress signals in voice, gestures or searches. It classifies these signals by severity and securely alerts the appropriate responders: NGOs, hospitals, or authorities.",
      'stats-title': "Key Statistics",
      'stat1': "1 suicide every 40 seconds",
      'stat1-desc': "worldwide",
      'stat2': "+30%",
      'stat2-desc': "higher chances of intervention if danger detected early",
      'stat3': "95%",
      'stat3-desc': "of users believe in AI's ethical potential",
      'contact-title': "Contact",
      'faq1': "Does the AI access private data?",
      'faq1-desc': "No. Silent Witness does not record any personal data...",
      'faq2': "How are alerts transmitted?",
      'faq2-desc': "Via a secure and encrypted database...",
      'faq3': "Is it already in service?",
      'faq3-desc': "Silent Witness is in advanced prototype phase...",
      'faq4': "Who can contact us?",
      'faq4-desc': "NGOs, hospitals, AI developers, researchers...",
    },
    ar: {
      'hero-title': "الذكاء الاصطناعي في خدمة الإنسان",
      'hero-desc': "الكشف الأخلاقي عن إشارات distress لإنقاذ الأرواح بسرية تامة.",
      'mission-title': "مهمتنا",
      'mission-desc': "Silent Witness هو حل ذكاء اصطناعي قادر على اكتشاف إشارات distress في الصوت، الحركات أو عمليات البحث. يصنف هذه الإشارات حسب الخطورة، ثم ينقل تنبيهًا آمنًا وأخلاقيًا للجهات المختصة: منظمات غير حكومية، مستشفيات، أو السلطات.",
      'stats-title': "إحصائيات رئيسية",
      'stat1': "انتحار واحد كل 40 ثانية",
      'stat1-desc': "حول العالم",
      'stat2': "+30%",
      'stat2-desc': "فرص التدخل إذا تم الكشف المبكر عن الخطر",
      'stat3': "95%",
      'stat3-desc': "من المستخدمين يؤمنون بالإمكانات الأخلاقية للذكاء الاصطناعي",
      'contact-title': "اتصل بنا",
      'faq1': "هل يصل الذكاء الاصطناعي إلى بيانات خاصة؟",
      'faq1-desc': "لا. لا يقوم Silent Witness بتسجيل أي بيانات شخصية...",
      'faq2': "كيف يتم إرسال التنبيهات؟",
      'faq2-desc': "عبر قاعدة بيانات مؤمنة ومشفرة...",
      'faq3': "هل هو قيد الخدمة بالفعل؟",
      'faq3-desc': "Silent Witness في مرحلة نموذج أولي متقدم...",
      'faq4': "من يمكنه الاتصال بنا؟",
      'faq4-desc': "المنظمات غير الحكومية، المستشفيات، مطورو الذكاء الاصطناعي، الباحثون...",
    }
  };

  // Function to update page text by lang
  function updateLanguage(lang) {
    for (const id in translations[lang]) {
      const el = document.getElementById(id);
      if (el) {
        el.textContent = translations[lang][id];
      }
    }

    // Adjust dir for Arabic
    if(lang === 'ar') {
      document.documentElement.dir = 'rtl';
      bodyEl.style.textAlign = 'right';
    } else {
      document.documentElement.dir = 'ltr';
      bodyEl.style.textAlign = 'left';
    }
  }

  // On language change
  langSelect.addEventListener('change', e => {
    updateLanguage(e.target.value);
    localStorage.setItem('language', e.target.value);
  });

  // Load saved language or default fr
  const savedLang = localStorage.getItem('language') || 'fr';
  langSelect.value = savedLang;
  updateLanguage(savedLang);

  // ==== CAROUSEL FUNCTIONALITY ====
  const track = document.querySelector('.carousel-track');
  const slides = Array.from(track.children);
  const prevBtn = document.querySelector('.carousel-button.prev');
  const nextBtn = document.querySelector('.carousel-button.next');
  let currentIndex = 0;

  function updateCarousel() {
    const slideWidth = slides[0].getBoundingClientRect().width;
    track.style.transform = `translateX(-${currentIndex * slideWidth}px)`;
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

  // ==== ANIMATED TEXT ====
  // Already done with CSS blinking cursor.

  // ==== EMAILJS FORM HANDLER ====
  // Assumes EmailJS SDK is loaded separately or via script tag
  // Replace your EmailJS user ID and template ID below:

  // To use EmailJS, add this script in your <head> or before </body>:
  // <script src="https://cdn.emailjs.com/sdk/3.2/email.min.js"></script>
  // emailjs.init('YOUR_PUBLIC_KEY');

  const contactForm = document.getElementById('contact-form');

  contactForm.addEventListener('submit', function(e) {
    e.preventDefault();

    // Simple validation already ensured by required attribute
    const formData = {
      from_name: contactForm.name.value,
      from_email: contactForm.email.value,
      message: contactForm.message.value
    };

    // Disable button to prevent multiple sends
    contactForm.querySelector('button[type="submit"]').disabled = true;

    emailjs.send('service_za2pm5i', 'template_mt5ycpk', formData)
      .then(() => {
        alert('Merci pour votre message ! Nous vous répondrons bientôt.');
        contactForm.reset();
      }, (error) => {
        alert('Erreur lors de l’envoi, veuillez réessayer plus tard.');
        console.error('EmailJS error:', error);
      })
      .finally(() => {
        contactForm.querySelector('button[type="submit"]').disabled = false;
      });
  });
</script>

<!-- Load EmailJS SDK -->
<script src="https://cdn.emailjs.com/sdk/3.2/email.min.js"></script>
<script>
  emailjs.init('_pR14KMi1syThzlmY'); // Remplace par ta clé publique EmailJS
</script>

</body>
</html>

