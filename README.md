<!DOCTYPE html>
<html lang="fr" >
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Silent Witness - Contact</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700;900&display=swap" rel="stylesheet" />

  <style>
    :root {
      --color-primary: #1c5980;
      --color-secondary: #8fc1a1;
      --color-bg-light: #f9fafb;
      --color-bg-dark: #121212;
      --color-text-light: #222;
      --color-text-dark: #e0e0e0;
      --input-bg: #fff;
      --input-bg-dark: #222;
      --transition-speed: 0.3s;
      --border-radius: 14px;
      --font-family: 'Poppins', sans-serif;
      --shadow-light: 0 8px 20px rgba(28, 89, 128, 0.2);
      --shadow-dark: 0 8px 20px rgba(0, 0, 0, 0.8);
    }
    body {
      margin: 0; padding: 0;
      font-family: var(--font-family);
      background-color: var(--color-bg-light);
      color: var(--color-text-light);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      transition: background-color var(--transition-speed), color var(--transition-speed);
    }
    body.dark-theme {
      background-color: var(--color-bg-dark);
      color: var(--color-text-dark);
    }
    main {
      flex-grow: 1;
      max-width: 1000px;
      margin: 2rem auto 4rem;
      padding: 0 1rem;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 2rem;
      align-items: center;
    }
    /* === Form styles === */
    form#contact-form {
      background: var(--input-bg);
      padding: 2rem 2.5rem;
      border-radius: var(--border-radius);
      box-shadow: var(--shadow-light);
      display: flex;
      flex-direction: column;
      gap: 1.4rem;
      transition: background-color var(--transition-speed), box-shadow var(--transition-speed);
    }
    body.dark-theme form#contact-form {
      background: var(--input-bg-dark);
      box-shadow: var(--shadow-dark);
    }
    h2 {
      font-weight: 900;
      font-size: 2.4rem;
      margin-bottom: 1rem;
      color: var(--color-primary);
      user-select: none;
      letter-spacing: 1.2px;
    }
    label {
      font-weight: 600;
      margin-bottom: 0.25rem;
      display: block;
      color: var(--color-primary);
    }
    input, textarea {
      font-family: var(--font-family);
      font-size: 1rem;
      padding: 0.9rem 1.2rem;
      border-radius: var(--border-radius);
      border: 2px solid #ccc;
      transition: border-color var(--transition-speed);
      resize: vertical;
      width: 100%;
      box-sizing: border-box;
      background: var(--input-bg);
      color: var(--color-text-light);
    }
    body.dark-theme input, body.dark-theme textarea {
      background: var(--input-bg-dark);
      color: var(--color-text-dark);
      border-color: #555;
    }
    input:focus, textarea:focus {
      border-color: var(--color-primary);
      outline: none;
      box-shadow: 0 0 10px rgba(28,89,128,0.4);
    }
    .error-msg {
      font-size: 0.85rem;
      color: #c0392b;
      font-weight: 600;
      margin-top: -0.8rem;
      margin-bottom: 0.6rem;
      display: none;
      user-select: none;
    }
    .error-msg.active {
      display: block;
    }
    button[type="submit"] {
      background: var(--color-primary);
      color: white;
      font-weight: 700;
      padding: 1.2rem;
      border: none;
      border-radius: var(--border-radius);
      cursor: pointer;
      transition: background-color 0.35s ease, color 0.35s ease;
      box-shadow: 0 6px 20px rgba(28, 89, 128, 0.35);
      font-size: 1.2rem;
      letter-spacing: 0.8px;
    }
    button[type="submit"]:hover {
      background: var(--color-secondary);
      color: var(--color-primary);
      box-shadow: 0 8px 28px rgba(143, 193, 161, 0.5);
    }

    /* Images container */
    .contact-image-container {
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
      justify-content: center;
      align-items: center;
      padding: 0 1rem;
    }
    .contact-image-container img {
      width: 100%;
      max-width: 380px;
      border-radius: var(--border-radius);
      box-shadow: var(--shadow-light);
      user-select: none;
      transition: transform 0.3s ease;
    }
    body.dark-theme .contact-image-container img {
      box-shadow: var(--shadow-dark);
    }
    .contact-image-container img:hover {
      transform: scale(1.05);
    }

    /* Langue selector top right */
    #lang-select {
      position: fixed;
      top: 1rem;
      right: 1rem;
      padding: 0.3rem 0.8rem;
      font-size: 1.1rem;
      border-radius: var(--border-radius);
      border: none;
      cursor: pointer;
      box-shadow: var(--shadow-light);
      transition: background-color 0.3s ease;
      background: white;
      color: var(--color-primary);
      z-index: 999;
    }
    #lang-select:hover, #lang-select:focus {
      background-color: var(--color-secondary);
      color: white;
      outline: none;
    }

    /* Responsive */
    @media (max-width: 900px) {
      main {
        grid-template-columns: 1fr;
        gap: 3rem;
      }
      .contact-image-container img {
        max-width: 100%;
      }
    }

    /* RTL support */
    html[lang="ar"] {
      direction: rtl;
    }
    html[lang="ar"] body {
      text-align: right;
    }
    html[lang="ar"] label {
      text-align: right;
    }
    html[lang="ar"] input, html[lang="ar"] textarea {
      direction: rtl;
      text-align: right;
    }
  </style>
</head>
<body>

  <select id="lang-select" aria-label="Select Language">
    <option value="fr" selected>Français</option>
    <option value="en">English</option>
    <option value="ar">العربية</option>
  </select>

  <main>
    <form id="contact-form" novalidate>
      <h2 data-lang-fr="Contactez-nous" data-lang-en="Contact Us" data-lang-ar="اتصل بنا">Contactez-nous</h2>

      <label for="name" data-lang-fr="Nom" data-lang-en="Name" data-lang-ar="الاسم">Nom</label>
      <input
        type="text"
        id="name"
        name="name"
        placeholder="Votre nom"
        required
        data-placeholder-fr="Votre nom"
        data-placeholder-en="Your name"
        data-placeholder-ar="اسمك"
        aria-describedby="name-error"
      />
      <div id="name-error" class="error-msg" aria-live="polite">Veuillez entrer votre nom.</div>

      <label for="email" data-lang-fr="Email" data-lang-en="Email" data-lang-ar="البريد الإلكتروني">Email</label>
      <input
        type="email"
        id="email"
        name="email"
        placeholder="Votre email"
        required
        data-placeholder-fr="Votre email"
        data-placeholder-en="Your email"
        data-placeholder-ar="بريدك الإلكتروني"
        aria-describedby="email-error"
      />
      <div id="email-error" class="error-msg" aria-live="polite">Veuillez entrer un email valide.</div>

      <label for="message" data-lang-fr="Message" data-lang-en="Message" data-lang-ar="رسالتك">Message</label>
      <textarea
        id="message"
        name="message"
        rows="5"
        placeholder="Votre message"
        required
        data-placeholder-fr="Votre message"
        data-placeholder-en="Your message"
        data-placeholder-ar="رسالتك"
        aria-describedby="message-error"
      ></textarea>
      <div id="message-error" class="error-msg" aria-live="polite">Le message ne peut pas être vide.</div>

      <button type="submit" data-lang-fr="Envoyer" data-lang-en="Send" data-lang-ar="إرسال">Envoyer</button>
    </form>

    <div class="contact-image-container" aria-hidden="true">
      <img
        src="https://images.unsplash.com/photo-1515377905703-c4788e51af15?auto=format&fit=crop&w=600&q=80"
        alt=""
        loading="lazy"
      />
      <img
        src="https://images.unsplash.com/photo-1551836022-d5d88e9218df?auto=format&fit=crop&w=600&q=80"
        alt=""
        loading="lazy"
      />
    </div>
  </main>

  <script>
    // === Gestion langue simple (FR / EN / AR) ===
    const langSelect = document.getElementById('lang-select');
    const allLangElems = document.querySelectorAll('[data-lang-fr]');

    function updateLanguage(lang) {
      document.documentElement.lang = lang;
      if (lang === 'ar') {
        document.documentElement.dir = 'rtl';
      } else {
        document.documentElement.dir = 'ltr';
      }

      allLangElems.forEach(el => {
        if (lang === 'fr' && el.dataset.langFr) el.textContent = el.dataset.langFr;
        else if (lang === 'en' && el.dataset.langEn) el.textContent = el.dataset.langEn;
        else if (lang === 'ar' && el.dataset.langAr) el.textContent = el.dataset.langAr;

        // placeholders
        if (el.placeholder) {
          if (lang === 'fr' && el.dataset.placeholderFr) el.placeholder = el.dataset.placeholderFr;
          else if (lang === 'en' && el.dataset.placeholderEn) el.placeholder = el.dataset.placeholderEn;
          else if (lang === 'ar' && el.dataset.placeholderAr) el.placeholder = el.dataset.placeholderAr;
        }
      });

      localStorage.setItem('preferredLang', lang);
    }

    // Initial language
    const savedLang = localStorage.getItem('preferredLang') || 'fr';
    langSelect.value = savedLang;
    updateLanguage(savedLang);

    langSelect.addEventListener('change', (e) => {
      updateLanguage(e.target.value);
    });

    // === Form validation ===
    const form = document.getElementById('contact-form');
    const nameInput = form.elements['name'];
    const emailInput = form.elements['email'];
    const messageInput = form.elements['message'];

    const nameError = document.getElementById('name-error');
    const emailError = document.getElementById('email-error');
    const messageError = document.getElementById('message-error');

    function validateName() {
      if (nameInput.value.trim().length < 2) {
        nameError.classList.add('active');
        return false;
      } else {
        nameError.classList.remove('active');
        return true;
      }
    }

    function validateEmail() {
      // Simple email regex
      const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!re.test(emailInput.value.trim())) {
        emailError.classList.add('active');
        return false;
      } else {
        emailError.classList.remove('active');
        return true;
      }
    }

    function validateMessage() {
      if (messageInput.value.trim().length < 5) {
        messageError.classList.add('active');
        return false;
      } else {
        messageError.classList.remove('active');
        return true;
      }
    }

    nameInput.addEventListener('input', validateName);
    emailInput.addEventListener('input', validateEmail);
    messageInput.addEventListener('input', validateMessage);

    form.addEventListener('submit', (e) => {
      e.preventDefault();

      const validName = validateName();
      const validEmail = validateEmail();
      const validMessage = validateMessage();

      if (validName && validEmail && validMessage) {
        // Envoi via Formspree (remplace "TON_EMAIL" ci-dessous par ton email Formspree)
        fetch('https://formspree.io/f/mlezwqyw', {
          method: 'POST',
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            name: nameInput.value.trim(),
            email: emailInput.value.trim(),
            message: messageInput.value.trim()
          })
        }).then(response => {
          if (response.ok) {
            alert({
              fr: "Message envoyé avec succès !",
              en: "Message sent successfully!",
              ar: "تم إرسال الرسالة بنجاح!"
            }[langSelect.value] || "Message sent!");
            form.reset();
          } else {
            alert({
              fr: "Erreur lors de l'envoi. Merci de réessayer.",
              en: "Error sending message. Please try again.",
              ar: "حدث خطأ أثناء الإرسال. حاول مرة أخرى."
            }[langSelect.value] || "Error sending message.");
          }
        }).catch(() => {
          alert({
            fr: "Erreur réseau. Merci de vérifier votre connexion.",
            en: "Network error. Please check your connection.",
            ar: "خطأ في الشبكة. يرجى التحقق من الاتصال."
          }[langSelect.value] || "Network error.");
        });
      }
    });
  </script>

</body>
</html>

