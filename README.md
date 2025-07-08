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
      max-width: 900px;
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
    iframe {
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
  </style>
  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script>
    emailjs.init('_pR14KMi1syThzlmY');

    function sendEmail(e) {
      e.preventDefault();
      emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', e.target)
        .then(() => alert('Message envoyé!'))
        .catch(error => alert('Erreur: ' + error));
    }

    con
