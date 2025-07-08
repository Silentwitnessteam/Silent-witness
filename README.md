<section class="section">
  <h2>Faire un don</h2>
  <p>Chaque contribution aide Silent Witness à protéger des vies grâce à l'IA. Merci pour votre soutien 💙</p>

  <!-- Script PayPal -->
  <script 
    src="https://www.paypal.com/sdk/js?client-id=BAAwNQmuQNtmwbB198XpnMFgJqBHvKNcvg138E9ddcIrNxHGCrGT2tvdVOyLaJTqde8dM-9e9ZglZUXS9A&components=hosted-buttons&disable-funding=venmo&currency=USD">
  </script>

  <!-- Container du bouton PayPal -->
  <div id="paypal-container-UTEPDMT9UCV2S"></div>

  <script>
    paypal.HostedButtons({
      hostedButtonId: "UTEPDMT9UCV2S",
    }).render("#paypal-container-UTEPDMT9UCV2S");
  </script>
</section>

<section class="section">
  <h2>Carte interactive des taux de suicide par pays</h2>
  <div id="map" style="height: 500px; width: 100%;"></div>

  <link
    rel="stylesheet"
    href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
    integrity="sha256-sA+e2Zb65+VZCjUaa1uXCjMQFS9Nn5oYo8g9JfUoA34="
    crossorigin=""
  />
  <script
    src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"
    integrity="sha256-o9N1j8Mk7R8C3LxG7nDw6b4R7m7JlH3dWusK5tDgnz8="
    crossorigin="">
  </script>
  <script>
    const suicideData = [
      { country: "France", lat: 46.2276, lng: 2.2137, rate: 12.1 },
      { country: "Japan", lat: 36.2048, lng: 138.2529, rate: 16.5 },
      { country: "USA", lat: 37.0902, lng: -95.7129, rate: 14.5 },
      { country: "Brazil", lat: -14.235, lng: -51.9253, rate: 6.3 },
      { country: "India", lat: 20.5937, lng: 78.9629, rate: 15.7 },
      { country: "Russia", lat: 61.524, lng: 105.3188, rate: 26.5 }
    ];

    const map = L.map('map').setView([20, 0], 2);

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '© OpenStreetMap contributors'
    }).addTo(map);

    suicideData.forEach(country => {
      const radius = country.rate * 20000;
      const color = country.rate > 20 ? '#b30000' : country.rate > 15 ? '#e67e00' : '#1c5980';
      L.circle([country.lat, country.lng], {
        color,
        fillColor: color,
        fillOpacity: 0.5,
        radius
      }).addTo(map)
        .bindPopup(`<strong>${country.country}</strong><br>Taux de suicide: ${country.rate} / 100k`);
    });
  </script>
</section>


