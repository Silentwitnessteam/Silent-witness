<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Silent Witness - IA au service de l'humain</title>
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap">
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: #f5f7fa;
      color: #1c5980;
      line-height: 1.5;
    }
    header {
      background-color: #1c5980;
      color: white;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    header strong {
      font-size: 1.5rem;
    }
    .lang-select {
      padding: 6px 12px;
      border-radius: 8px;
      border: 2px solid #8fc1a1;
      background-color: white;
      font-weight: 600;
      cursor: pointer;
    }
    .hero {
      padding: 4rem 2rem;
      background: linear-gradient(to right, #1c5980, #8fc1a1);
      color: white;
      text-align: center;
    }
    .hero h1 {
      font-size: 2.5rem;
    }
    .hero p {
      font-size: 1.2rem;
    }
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
    }
    .carousel-slide img {
      width: 100%;
      height: auto;
      display: block;
      border-radius: 12px;
    }
    .carousel-button {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      background: #1c5980cc;
      color: white;
      font-size: 2rem;
      border: none;
      border-radius: 50%;
      cursor: pointer;
    }
    .carousel-button.prev { left: 10px; }
    .carousel-button.next { right: 10px; }
    .whitepaper-download-button {
      background-color: #1c5980;
      color: white;
      font-weight: bold;
      font-size: 1rem;
      padding: 12px 24px;
      border-radius: 10px;
      text-decoration: none;
      display: inline-block;
      margin-top: 1.5rem;
    }
    footer {
      text-align: center;
      padding: 1rem;
      background: #1c5980;
      color: white;
      font-size: 0.9rem;
    }
    .animated-text {
      animation: pulseText 2s infinite;
    }
    @keyframes pulseText {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.6; transform: scale(1.05); }
    }
  </style>
</head>
<body>
  <header>
    <strong>Silent Witness</strong>
    <select class="lang-select" id="lang-select">
      <option value="fr">🇫🇷 Français</option>
      <option value="en">🇬🇧 English</option>
      <option value="ar">🇸🇦 العربية</option>
    </select>
  </header>

  <section class="hero">
    <h1 id="hero-title">L'IA au service de l'humain</h1>
    <p id="hero-desc">Détection éthique des signaux de détresse, pour sauver des vies en toute confidentialité.</p>
  </section>

  <section id="carousel" class="carousel">
    <button class="carousel-button prev">&#10094;</button>
    <div class="carousel-track">
      <div class="carousel-slide">
        <img src="https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=800&q=80" alt="Homme avec un casque de réalité augmentée">
      </div>
      <div class="carousel-slide">
        <img src="https://images.unsplash.com/photo-1497493292307-31c376b6e479?auto=format&fit=crop&w=800&q=80" alt="Femme et robot collaborant ensemble">
      </div>
    </div>
    <button class="carousel-button next">&#10095;</button>
  </section>

  <section id="whitepaper" style="text-align:center; margin: 4rem auto;">
    <h2 id="whitepaper-title"><span class="animated-text">You're not alone</span></h2>
    <p id="whitepaper-desc">Découvrez notre livre blanc complet sur Silent Witness : une IA éthique dédiée à la prévention et à la protection des plus vulnérables.</p>
    <a href="https://silentwitnessteam.github.io/Silent-witness/Silent_Witness_White_Paper.pdf" target="_blank" class="whitepaper-download-button">📘 Télécharger notre White Paper</a>
  </section>

  <section id="contact" style="max-width: 500px; margin: auto; padding: 2rem;">
    <h2 id="contact-title">Contact</h2>
    <form id="contact-form">
      <label for="name">Nom:</label>
      <input type="text" id="name" name="name" required><br><br>

      <label for="email">Email:</label>
      <input type="email" id="email" name="email" required><br><br>

      <label for="message">Message:</label><br>
      <textarea id="message" name="message" rows="5" required></textarea><br><br>

      <button type="submit">Envoyer</button>
    </form>
  </section>

  <footer>
    © 2025 Silent Witness — IA pour la prévention, l'éthique et la vie.
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
  <script>
    emailjs.init('_pR14KMi1syThzlmY');

    document.getElementById('contact-form').addEventListener('submit', function(event) {
      event.preventDefault();
      emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', this)
        .then(() => alert('Message envoyé avec succès!'))
        .catch((error) => alert('Erreur: ' + error.text));
    });
  </script>
</body>
</html>

