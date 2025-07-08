<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Silent Witness</title>
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background-color: var(--bg-color, #ffffff);
      color: var(--text-color, #1c5980);
      transition: background 0.3s, color 0.3s;
    }
    .dark-theme {
      --bg-color: #1c1c1c;
      --text-color: #f0f0f0;
    }
    header {
      padding: 1rem;
      background: #204d7a;
      color: white;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .language-select, .theme-toggle {
      margin: 0 10px;
    }
    .animated-text {
      font-size: 2rem;
      font-weight: bold;
      text-align: center;
      margin: 2rem 0;
      animation: pulseText 2s infinite;
    }
    @keyframes pulseText {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.6; transform: scale(1.05); }
    }
    .section {
      padding: 2rem;
      max-width: 1200px;
      margin: auto;
    }
    .download-btn {
      display: inline-block;
      background: #1c5980;
      color: white;
      padding: 0.8rem 1.5rem;
      border-radius: 8px;
      text-decoration: none;
      font-weight: bold;
      transition: 0.3s;
    }
    .download-btn:hover {
      background: #8fc1a1;
      color: #1c5980;
    }
    iframe, .responsive-map {
      width: 100%;
      height: 500px;
      border: none;
      margin-top: 2rem;
    }
    form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      margin-top: 2rem;
    }
    input, textarea {
      padding: 0.8rem;
      border-radius: 6px;
      border: 1px solid #ccc;
    }
    button {
      padding: 0.8rem;
      background: #204d7a;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }
    .image-banner {
      width: 100%;
      max-height: 400px;
      object-fit: cover;
      margin-top: 1rem;
    }
  </style>
  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script src="https://www.paypal.com/sdk/js?client-id=BAAwNQmuQNtmwbB198XpnMFgJqBHvKNcvg138E9ddcIrNxHGCrGT2tvdVOyLaJTqde8dM-9e9ZglZUXS9A&components=hosted-buttons&disable-funding=venmo&currency=USD"></script>
  <script>
    emailjs.init('_pR14KMi1syThzlmY');
    function sendEmail(e) {
      e.preventDefault();
      emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', e.target)
        .then(() => alert('Message envoyé!'))
        .catch(error => alert('Erreur: ' + error));
    }
    const translations = {
      fr: {
        title: "Vous n'êtes pas seul",
        whitepaper: "📘 Télécharger notre White Paper",
        paragraph: "Découvrez notre livre blanc sur Silent Witness : une IA éthique dédiée à la détection de détresse émotionnelle et à la prévention du suicide.",
        stats: [
          "Près de 800 000 personnes se suicident chaque année (OMS)",
          "1 suicide toutes les 40 secondes dans le monde",
          "La majorité des victimes n'expriment pas leur souffrance à temps",
          "Une grande part liée à des conflits conjugaux ou à la solitude"
        ]
      },
      en: {
        title: "You're not alone",
        whitepaper: "📘 Download our White Paper",
        paragraph: "Explore our white paper on Silent Witness – an ethical AI to detect emotional distress and prevent suicide.",
        stats: [
          "Nearly 800,000 people die by suicide every year (WHO)",
          "One suicide every 40 seconds worldwide",
          "Most victims don’t express their suffering in time",
          "Often linked to domestic issues or loneliness"
        ]
      },
      ar: {
        title: "لست وحدك",
        whitepaper: "📘 تحميل الورقة البيضاء",
        paragraph: "اكتشف الورقة البيضاء لـ Silent Witness - ذكاء اصطناعي أخلاقي للكشف عن الضيق العاطفي والوقاية من الانتحار.",
        stats: [
          "حوالي 800,000 حالة انتحار سنويًا (منظمة الصحة العالمية)",
          "انتحار واحد كل 40 ثانية في العالم",
          "معظم الضحايا لا يعبرون عن معاناتهم في الوقت المناسب",
          "غالبًا ما تكون الأسباب مشاكل زوجية أو وحدة"
        ]
      }
    };
    function updateLanguage(lang) {
      document.querySelector('.animated-text').textContent = translations[lang].title;
      document.getElementById('wp-paragraph').textContent = translations[lang].paragraph;
      document.getElementById('wp-btn').textContent = translations[lang].whitepaper;
      const statsList = document.getElementById('stats-list');
      statsList.innerHTML = '';
      translations[lang].stats.forEach(stat => {
        const li = document.createElement('li');
        li.textContent = stat;
        statsList.appendChild(li);
      });
    }
    function toggleTheme() {
      document.body.classList.toggle('dark-theme');
    }
    window.onload = () => {
      document.getElementById('contact-form').addEventListener('submit', sendEmail);
      document.getElementById('lang-select').addEventListener('change', (e) => updateLanguage(e.target.value));
      document.getElementById('theme-toggle').addEventListener('click', toggleTheme);
      updateLanguage('fr');
    }
  </script>
</head>
<body>
  <header>
    <h1>Silent Witness</h1>
    <div>
      <select id="lang-select" class="language-select">
        <option value="fr">Français</option>
        <option value="en">English</option>
        <option value="ar">العربية</option>
      </select>
      <button id="theme-toggle" class="theme-toggle">🌓</button>
    </div>
  </header>

  <div class="animated-text"></div>

  <img src="https://images.unsplash.com/photo-1605198681904-0f3d7d2d7e9a" alt="IA et détresse humaine" class="image-banner" />

  <section class="section">
    <p id="wp-paragraph"></p>
    <a id="wp-btn" href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf" target="_blank" class="download-btn"></a>
  </section>

  <section class="section">
    <h2>Carte mondiale des suicides</h2>
    <iframe class="responsive-map" src="https://ourworldindata.org/grapher/suicide-rate-by-country?tab=map" allowfullscreen></iframe>
  </section>

  <section class="section">
    <h2>Statistiques clés</h2>
    <ul id="stats-list"></ul>
  </section>

  <section class="section">
    <h2>Étapes de détection IA</h2>
    <ol>
      <li>Analyse des mots clés dans les messages, requêtes IA ou recherches web</li>
      <li>Corrélation des données vocales, textuelles ou comportementales</li>
      <li>Évaluation automatique du niveau de détresse</li>
      <li>Classement de l’urgence (vert / orange / rouge)</li>
      <li>Déclenchement d'une alerte vers ONG, autorités ou hôpitaux selon le niveau</li>
    </ol>
  </section>

  <section class="section">
    <h2>Faire un don pour soutenir le projet</h2>
    <div id="paypal-container-UTEPDMT9UCV2S"></div>
    <script>
      paypal.HostedButtons({
        hostedButtonId: "UTEPDMT9UCV2S",
      }).render("#paypal-container-UTEPDMT9UCV2S");
    </script>
  </section>

  <section class="section">
    <h2>Contact</h2>
    <form id="contact-form">
      <input type="text" name="nom" placeholder="Votre nom" required>
      <input type="email" name="email" placeholder="Votre email" required>
      <textarea name="message" rows="4" placeholder="Votre message" required></textarea>
      <button type="submit">Envoyer</button>
    </form>
  </section>
</body>
</html>
