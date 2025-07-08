
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

  /* === Detection Process Animation === */
  .detection-process {
    margin-top: 1rem;
    font-weight: 700;
    color: #004d7a;
    user-select: none;
  }
  body[data-theme='dark'] .detection-process {
    color: #7ec8e3;
  }

  .progress-bar {
    position: relative;
    width: 100%;
    height: 8px;
    background: #cde6f7;
    border-radius: 5px;
    overflow: hidden;
    margin-bottom: 0.75rem;
  }
  body[data-theme='dark'] .progress-bar {
    background: #23415a;
  }

  .progress-fill {
    height: 100%;
    width: 0;
    background: #004d7a;
    border-radius: 5px;
    transition: width 1s ease;
  }
  body[data-theme='dark'] .progress-fill {
    background: #7ec8e3;
  }

  .steps {
    display: flex;
    justify-content: space-between;
    padding: 0;
    margin: 0;
    list-style: none;
    font-size: 1rem;
  }
  .step {
    flex: 1;
    text-align: center;
    opacity: 0.4;
    transition: opacity 0.3s ease, color 0.3s ease;
  }
  .step.active {
    opacity: 1;
    color: inherit;
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
    <div class="detection-process" aria-label="Animation du processus de détection de détresse" role="region" aria-live="polite">
      <div class="progress-bar">
        <div class="progress-fill"></div>
      </div>
      <ul class="steps">
        <li class="step active" data-step="Analyse vocale">🎙️ Analyse vocale</li>
        <li class="step" data-step="Analyse des gestes">🖐️ Analyse des gestes</li>
        <li class="step" data-step="Analyse des recherches">🔍 Analyse des recherches</li>
        <li class="step" data-step="Détection terminée">✅ Détection terminée</li>
      </ul>
    </div>
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
          <img src="https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=800&q=80" alt="Main humaine et circuit imprimé" />
        </div>
        <div class="carousel-slide">
          <img src="https://images.unsplash.com/photo-1549924231-f129b911e442?auto=format&fit=crop&w=800&q=80" alt="Ondes sonores abstraites" />
        </div>
      </div>
      <button class="carousel-button next" aria-label="Image suivante">&#10095;</button>
    </div>
  </section>

  <section id="whitepaper">
    <h2>White Paper</h2>
    <p>Téléchargez notre document détaillé sur la technologie et l’éthique du projet.</p>
    <a href="silent-witness-whitepaper.pdf" class="btn" target="_blank" rel="noopener">Télécharger le PDF</a>
  </section>

  <section id="contact">
    <h2>Contactez-nous</h2>
    <form id="contact-form">
      <label for="name">Nom complet</label>
      <input type="text" id="name" name="name" placeholder="Votre nom" required />
      <label for="email">Email</label>
      <input type="email" id="email" name="email" placeholder="exemple@mail.com" required />
      <label for="message">Message</label>
      <textarea id="message" name="message" rows="5" placeholder="Votre message" required></textarea>
      <button type="submit">Envoyer</button>
    </form>
    <div id="form-status" role="alert" aria-live="polite" style="margin-top:1rem;"></div>
  </section>
</main>

<footer>
  &copy; 2025 Silent Witness. Tous droits réservés.
</footer>

<script>
  // === THEME TOGGLE ===
  const themeToggleBtn = document.getElementById('theme-toggle');
  themeToggleBtn.addEventListener('click', () => {
    const currentTheme = document.body.getAttribute('data-theme');
    if (currentTheme === 'light') {
      document.body.setAttribute('data-theme', 'dark');
    } else {
      document.body.setAttribute('data-theme', 'light');
    }
  });

  // === LANGUAGE SELECTOR ===
  const langSelect = document.getElementById('lang-select');

  // Texts multilingues simplifiés
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
      'contact-title': "Contactez-nous",
      'name-label': "Nom complet",
      'email-label': "Email",
      'message-label': "Message",
      'submit-btn': "Envoyer",
      'whitepaper-title': "White Paper",
      'whitepaper-desc': "Téléchargez notre document détaillé sur la technologie et l’éthique du projet.",
      'whitepaper-btn': "Télécharger le PDF",
    },
    en: {
      'hero-title': "AI Serving Humanity",
      'hero-desc': "Ethical detection of distress signals to save lives confidentially.",
      'mission-title': "Our Mission",
      'mission-desc': "Silent Witness is an AI solution able to detect distress signals in voice, gestures, or searches of an individual. It classifies these signals by severity, then transmits an ethical and secure alert to appropriate responders: NGOs, hospitals, or authorities.",
      'stats-title': "Key Statistics",
      'stat1': "1 suicide every 40 seconds",
      'stat1-desc': "worldwide",
      'stat2': "+30%",
      'stat2-desc': "chance of intervention if danger is detected early",
      'stat3': "95%",
      'stat3-desc': "of users believe in AI's ethical potential",
      'contact-title': "Contact Us",
      'name-label': "Full Name",
      'email-label': "Email",
      'message-label': "Message",
      'submit-btn': "Send",
      'whitepaper-title': "White Paper",
      'whitepaper-desc': "Download our detailed document on the technology and ethics of the project.",
      'whitepaper-btn': "Download PDF",
    },
    ar: {
      'hero-title': "الذكاء الاصطناعي في خدمة الإنسان",
      'hero-desc': "الكشف الأخلاقي عن إشارات الضيق لإنقاذ الأرواح بسرية تامة.",
      'mission-title': "مهمتنا",
      'mission-desc': "Silent Witness هو حل ذكاء اصطناعي قادر على اكتشاف إشارات الضيق في الصوت والحركات والبحث لدى الفرد. يصنف هذه الإشارات حسب الخطورة ثم يرسل إنذارًا أخلاقيًا وآمنًا إلى الجهات المختصة: المنظمات، المستشفيات، أو السلطات.",
      'stats-title': "الإحصائيات الرئيسية",
      'stat1': "انتحار كل 40 ثانية",
      'stat1-desc': "في جميع أنحاء العالم",
      'stat2': "+30%",
      'stat2-desc': "فرصة التدخل إذا تم الكشف المبكر عن الخطر",
      'stat3': "95%",
      'stat3-desc': "من المستخدمين يؤمنون بإمكانات الذكاء الاصطناعي الأخلاقية",
      'contact-title': "اتصل بنا",
      'name-label': "الاسم الكامل",
      'email-label': "البريد الإلكتروني",
      'message-label': "الرسالة",
      'submit-btn': "إرسال",
      'whitepaper-title': "الوثيقة التقنية",
      'whitepaper-desc': "قم بتنزيل مستندنا التفصيلي حول التكنولوجيا وأخلاقيات المشروع.",
      'whitepaper-btn': "تحميل PDF",
    }
  };

  function updateTexts(lang) {
    document.getElementById('hero-title').textContent = translations[lang]['hero-title'];
    document.getElementById('hero-desc').textContent = translations[lang]['hero-desc'];
    document.getElementById('mission-title').textContent = translations[lang]['mission-title'];
    document.getElementById('mission-desc').textContent = translations[lang]['mission-desc'];
    document.getElementById('stats-title').textContent = translations[lang]['stats-title'];
    document.getElementById('stat1').textContent = translations[lang]['stat1'];
    document.getElementById('stat1-desc').textContent = translations[lang]['stat1-desc'];
    document.getElementById('stat2').textContent = translations[lang]['stat2'];
    document.getElementById('stat2-desc').textContent = translations[lang]['stat2-desc'];
    document.getElementById('stat3').textContent = translations[lang]['stat3'];
    document.getElementById('stat3-desc').textContent = translations[lang]['stat3-desc'];
    document.querySelector('#contact h2').textContent = translations[lang]['contact-title'];
    document.querySelector('label[for="name"]').textContent = translations[lang]['name-label'];
    document.querySelector('label[for="email"]').textContent = translations[lang]['email-label'];
    document.querySelector('label[for="message"]').textContent = translations[lang]['message-label'];
    document.querySelector('button[type="submit"]').textContent = translations[lang]['submit-btn'];
    document.querySelector('#whitepaper h2').textContent = translations[lang]['whitepaper-title'];
    document.querySelector('#whitepaper p').textContent = translations[lang]['whitepaper-desc'];
    document.querySelector('#whitepaper a').textContent = translations[lang]['whitepaper-btn'];
  }

  langSelect.addEventListener('change', () => {
    updateTexts(langSelect.value);
  });

  // Initialize default language texts
  updateTexts(langSelect.value);

  // === THEME TOGGLE (save preference) ===
  // Optionally save theme in localStorage for persistence
  if(localStorage.getItem('theme')) {
    document.body.setAttribute('data-theme', localStorage.getItem('theme'));
  }
  themeToggleBtn.addEventListener('click', () => {
    let currentTheme = document.body.getAttribute('data-theme');
    let newTheme = currentTheme === 'light' ? 'dark' : 'light';
    document.body.setAttribute('data-theme', newTheme);
    localStorage.setItem('theme', newTheme);
  });

  // === CAROUSEL ===
  const track = document.querySelector('.carousel-track');
  const slides = Array.from(track.children);
  const prevButton = document.querySelector('.carousel-button.prev');
  const nextButton = document.querySelector('.carousel-button.next');
  let currentIndex = 0;

  function updateCarousel() {
    const slideWidth = slides[0].getBoundingClientRect().width;
    track.style.transform = 'translateX(' + (-slideWidth * currentIndex) + 'px)';
  }

  prevButton.addEventListener('click', () => {
    currentIndex = (currentIndex - 1 + slides.length) % slides.length;
    updateCarousel();
  });
  nextButton.addEventListener('click', () => {
    currentIndex = (currentIndex + 1) % slides.length;
    updateCarousel();
  });

  // Auto rotate carousel every 5 sec
  setInterval(() => {
    currentIndex = (currentIndex + 1) % slides.length;
    updateCarousel();
  }, 5000);

  // === Detection Process Animation ===
  const steps = document.querySelectorAll('.detection-process .step');
  const progressFill = document.querySelector('.progress-fill');
  let currentStep = 0;
  const totalSteps = steps.length;

  function updateDetectionProcess() {
    steps.forEach((step, i) => {
      step.classList.toggle('active', i === currentStep);
    });
    const percent = (currentStep) / (totalSteps - 1) * 100;
    progressFill.style.width = percent + '%';
    currentStep = (currentStep + 1) % totalSteps;
  }
  updateDetectionProcess();
  setInterval(updateDetectionProcess, 2500);

  // === EMAILJS FORM ===
  // Remplace service_id, template_id et public_key par tes vraies clés EmailJS
  const serviceID = 'service_za2pm5i';
  const templateID = 'template_mt5ycpk';
  const publicKey = '_pR14KMi1syThzlmY';

  const form = document.getElementById('contact-form');
  const statusDiv = document.getElementById('form-status');

  form.addEventListener('submit', function(e) {
    e.preventDefault();
    statusDiv.textContent = "Envoi en cours...";
    const templateParams = {
      from_name: form.name.value,
      from_email: form.email.value,
      message: form.message.value
    };
    emailjs.send(serviceID, templateID, templateParams, publicKey)
      .then(() => {
        statusDiv.textContent = "Message envoyé avec succès ! Merci.";
        form.reset();
      }, (err) => {
        statusDiv.textContent = "Erreur lors de l'envoi, veuillez réessayer.";
        console.error('EmailJS error:', err);
      });
  });

</script>

<!-- EmailJS SDK -->
<script src="https://cdn.emailjs.com/dist/email.min.js"></script>
<script>
  (function(){
    emailjs.init('_pR14KMi1syThzlmY');
  })();
</script>

</body>
</html>
