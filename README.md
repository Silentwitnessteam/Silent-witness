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
    }
    #map {
      height: 100vh;
      width: 100%;
    }
    .counter {
      position: absolute;
      top: 10px;
      right: 10px;
      background: rgba(0,0,0,0.7);
      color: white;
      padding: 10px 20px;
      border-radius: 8px;
      font-size: 1.2rem;
      z-index: 1000;
    }
    .legend {
      position: absolute;
      bottom: 30px;
      left: 10px;
      background: white;
      padding: 10px;
      border-radius: 5px;
      font-size: 0.9rem;
      box-shadow: 0 2px 6px rgba(0,0,0,0.2);
    }
    .legend div {
      margin-bottom: 5px;
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
    .banner p {
      font-size: 1.2rem;
      margin-top: 1rem;
    }
    .image-row {
      display: flex;
      justify-content: center;
      gap: 20px;
      margin: 2rem;
    }
    .image-row img {
      width: 300px;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.3);
    }
  </style>
</head>
<body>
  <div class="banner">
    <h1>Vous n'êtes pas seul • You're not alone • لست وحدك</h1>
    <p>Un projet d'IA éthique pour détecter et protéger les personnes en détresse émotionnelle, psychologique ou sociale.</p>
  </div>

  <div class="image-row">
    <img src="https://images.unsplash.com/photo-1588091222431-31c148d5d2a4" alt="Humain et IA main dans la main">
    <img src="https://images.unsplash.com/photo-1593642532973-d31b6557fa68" alt="Interface IA empathique">
  </div>

  <div id="map"></div>
  <div class="counter" id="suicide-counter">🕯️ 0 suicides depuis l'ouverture</div>
  <div class="legend">
    <strong>Légende :</strong><br>
    <div><span style="background:red;width:12px;height:12px;display:inline-block;margin-right:5px;"></span> Taux élevé</div>
    <div><span style="background:orange;width:12px;height:12px;display:inline-block;margin-right:5px;"></span> Taux modéré</div>
    <div><span style="background:green;width:12px;height:12px;display:inline-block;margin-right:5px;"></span> Taux faible</div>
  </div>

  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <script>
    const map = L.map('map').setView([20, 0], 2);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; OpenStreetMap contributors'
    }).addTo(map);

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

    for (const [name, coord] of Object.entries(continents)) {
      const rate = suicideRates[name];
      const color = rate > 12 ? 'red' : rate > 8 ? 'orange' : 'green';
      L.circle(coord, {
        color,
        fillColor: color,
        fillOpacity: 0.5,
        radius: 1000000
      }).addTo(map).bindPopup(`<b>${name}</b><br>Taux de suicide : ${rate}/100k`);
    }

    let counter = 0;
    setInterval(() => {
      counter++;
      document.getElementById('suicide-counter').innerText = `🕯️ ${counter} suicides depuis l'ouverture`;
    }, 40000);
  </script>
</body>
</html>


