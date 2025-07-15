<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Silent Witness - Détection de détresse humaine</title>
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background-color: #f5f5f5;
      color: #1c1c1c;
      direction: ltr;
    }
    html[lang="ar"] body {
      direction: rtl;
      font-family: 'Cairo', sans-serif;
    }
    #map {
      height: 80vh;
      width: 100%;
    }
    .counter {
      text-align: center;
      margin: 1rem;
      font-weight: bold;
    }
    .legend, .filters {
      background: white;
      padding: 1rem;
      margin: 1rem auto;
      max-width: 900px;
      border-radius: 10px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }
    .legend div, .filters button {
      margin: 0.5rem 0;
    }
    .filters {
      text-align: center;
    }
    .filters button {
      padding: 0.5rem 1rem;
      margin: 0.2rem;
      border: none;
      border-radius: 6px;
      background: #204d7a;
      color: white;
      cursor: pointer;
    }
    .banner {
      text-align: center;
      padding: 2rem;
      background: linear-gradient(135deg, #204d7a, #8fc1a1);
      color: white;
    }
    .banner h1 {
      font-size: 2.5rem;
      margin: 0;
    }
    .paypal-section {
      text-align: center;
      margin: 3rem auto;
    }
    .contact-section {
      padding: 2rem;
      max-width: 800px;
      margin: auto;
    }
    .contact-section form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
    input, textarea {
      padding: 0.8rem;
      border-radius: 6px;
      border: 1px solid #ccc;
    }
    button[type="submit"] {
      background: #204d7a;
      color: white;
      border: none;
      padding: 0.8rem;
      border-radius: 6px;
      cursor: pointer;
    }
  </style>
  <script src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <script src="https://www.paypal.com/sdk/js?client-id=BAAwNQmuQNtmwbB198XpnMFgJqBHvKNcvg138E9ddcIrNxHGCrGT2tvdVOyLaJTqde8dM-9e9ZglZUXS9A&components=hosted-buttons&disable-funding=venmo&currency=USD"></script>
</head>
<body>
  <div class="banner">
    <h1>Vous n'êtes pas seul • You're not alone • لست وحدك</h1>
    <p>Un projet d'IA éthique pour détecter et protéger les personnes en détresse émotionnelle, psychologique ou sociale.</p>
  </div>

  <div class="filters">
    <strong>Filtrer par :</strong><br>
    <button onclick="filterMap('all')">Tous</button>
    <button onclick="filterMap('male')">Hommes</button>
    <button onclick="filterMap('female')">Femmes</button>
    <button onclick="filterMap('youth')">Jeunes</button>
    <button onclick="filterMap('violence')">Violences conjugales</button>
  </div>

  <div id="map"></div>
  <div class="counter" id="suicide-counter">🕯️ 0 suicides estimés depuis ouverture</div>

  <div class="legend">
    <strong>Légende des couleurs :</strong><br>
    <div><span style="background:red;width:12px;height:12px;display:inline-block;margin-right:5px;"></span> Taux élevé</div>
    <div><span style="background:orange;width:12px;height:12px;display:inline-block;margin-right:5px;"></span> Taux modéré</div>
    <div><span style="background:green;width:12px;height:12px;display:inline-block;margin-right:5px;"></span> Taux faible</div>
  </div>

  <div class="paypal-section">
    <h2>Soutenir le projet</h2>
    <div id="paypal-container-UTEPDMT9UCV2S"></div>
    <script>
      paypal.HostedButtons({
        hostedButtonId: "UTEPDMT9UCV2S"
      }).render("#paypal-container-UTEPDMT9UCV2S")
    </script>
  </div>

  <section class="contact-section">
    <h2>Contactez-nous</h2>
    <form id="contact-form">
      <input type="text" name="nom" placeholder="Votre nom" required>
      <input type="email" name="email" placeholder="Votre email" required>
      <textarea name="message" rows="4" placeholder="Votre message" required></textarea>
      <button type="submit">Envoyer</button>
    </form>
  </section>

  <script>
    emailjs.init('_pR14KMi1syThzlmY');
    document.getElementById('contact-form').addEventListener('submit', function(e) {
      e.preventDefault();
      emailjs.sendForm('service_za2pm5i', 'template_mt5ycpk', this)
        .then(() => alert('Message envoyé!'))
        .catch(error => alert('Erreur: ' + error));
    });

    const suicideRates = {
      "Africa": 11.0,
      "Asia": 14.2,
      "Europe": 13.5,
      "North America": 9.2,
      "South America": 6.4,
      "Oceania": 10.1
    };
    const continents = {
      "Africa": [0, 20],
      "Asia": [30, 30],
      "Europe": [55, 15],
      "North America": [40, -100],
      "South America": [-15, -60],
      "Oceania": [-25, 140]
    };
    const markers = [];

    const map = L.map('map').setView([20, 0], 2);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; OpenStreetMap contributors'
    }).addTo(map);

    for (const [name, coord] of Object.entries(continents)) {
      const rate = suicideRates[name];
      const color = rate > 12 ? 'red' : rate > 8 ? 'orange' : 'green';
      const marker = L.circle(coord, {
        color,
        fillColor: color,
        fillOpacity: 0.5,
        radius: 1000000
      }).addTo(map).bindPopup(`<b>${name}</b><br>Taux de suicide : ${rate}/100k`);
      markers.push(marker);
    }

    function filterMap(type) {
      alert("Filtrage par: " + type + " (fonction illustrative)");
      // Simulation : en vrai, on filtrerait les données à afficher ici
    }

    let counter = 0;
    setInterval(() => {
      counter++;
      document.getElementById('suicide-counter').innerText = `🕯️ ${counter} suicides estimés depuis ouverture`;
    }, 40000);
  </script>
</body>
</html>
