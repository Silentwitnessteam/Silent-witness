<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Silent Witness - Détection de détresse humaine</title>
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">
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
    body.dark {
      background-color: #1c1c1c;
      color: #f5f5f5;
    }
    body.dark .filters button,
    body.dark button[type="submit"] {
      background: #444;
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
    .controls {
      margin-top: 1rem;
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
    .image-section {
      text-align: center;
      margin: 2rem auto;
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
    <div class="controls">
      <select id="language-selector" onchange="changeLanguage(this.value)">
        <option value="fr">Français</option>
        <option value="en">English</option>
        <option value="ar">العربية</option>
      </select>
      <button onclick="toggleTheme()">🌓 Thème</button>
    </div>
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

  <div class="image-section">
    <img src="https://images.unsplash.com/photo-1524312000000-bdd3b7ab8ef5" alt="Détresse émotionnelle" style="width:100%;max-width:600px;border-radius:10px;">
    <p>Sensibilisation à la souffrance invisible</p>
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

    function changeLanguage(lang) {
      document.documentElement.lang = lang;
      location.reload();
    }

    function toggleTheme() {
      document.body.classList.toggle("dark");
    }

    const dataPoints = [
      { name: "Africa", coord: [0, 20], rate: 11.0, type: 'male' },
      { name: "Asia", coord: [30, 30], rate: 14.2, type: 'female' },
      { name: "Europe", coord: [55, 15], rate: 13.5, type: 'violence' },
      { name: "North America", coord: [40, -100], rate: 9.2, type: 'youth' },
      { name: "South America", coord: [-15, -60], rate: 6.4, type: 'female' },
      { name: "Oceania", coord: [-25, 140], rate: 10.1, type: 'male' }
    ];

    const map = L.map('map').setView([20, 0], 2);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; OpenStreetMap contributors'
    }).addTo(map);

    const markers = [];

    function createMarkers() {
      dataPoints.forEach(point => {
        const color = point.rate > 12 ? 'red' : point.rate > 8 ? 'orange' : 'green';
        const marker = L.circle(point.coord, {
          color,
          fillColor: color,
          fillOpacity: 0.5,
          radius: 1000000
        }).addTo(map).bindPopup(`<b>${point.name}</b><br>${point.type}<br>${point.rate}/100k`);
        marker.type = point.type;
        markers.push(marker);
      });
    }

    function filterMap(type) {
      markers.forEach(marker => {
        if (type === 'all' || marker.type === type) {
          marker.addTo(map);
        } else {
          map.removeLayer(marker);
        }
      });
    }

    createMarkers();

    let counter = 0;
    setInterval(() => {
      counter++;
      document.getElementById('suicide-counter').innerText = `🕯️ ${counter} suicides estimés depuis ouverture`;
    }, 40000);
  </script>
</body>
</html>
