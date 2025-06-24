# Sugar-belt
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Analysis of Clustered Points in Migori/Transmara Region</title>
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.3/dist/leaflet.css" />
  <style>
    #map { height: 600px; width: 100%; }
  </style>
</head>
<body>
  <div id="map"></div>
  <script src="https://unpkg.com/leaflet@1.9.3/dist/leaflet.js"></script>
  <script src="https://unpkg.com/leaflet.heat@0.2.0/dist/leaflet-heat.js"></script>
  <script>
    // Initialize the map
    var map = L.map('map').setView([-1.02, 34.65], 10);

    // Add CartoDB.Positron base layer
    L.tileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors &copy; <a href="https://carto.com/attributions">CARTO</a>',
      subdomains: 'abcd',
      maxZoom: 19
    }).addTo(map);

    // Add GeoJSON markers
    var geojsonData = {
      "type": "FeatureCollection",
      "features": [
        { "type": "Feature", "properties": { "marker-color": "#ff0000", "marker-size": "medium", "marker-symbol": "star", "title": "Nyaoke CBC" }, "geometry": { "type": "Point", "coordinates": [34.586, -0.8145] } },
        { "type": "Feature", "properties": { "marker-color": "#ff0000", "marker-size": "medium", "marker-symbol": "star", "title": "Chawgiwadu CBC" }, "geometry": { "type": "Point", "coordinates": [34.555, -0.902] } },
        { "type": "Feature", "properties": { "marker-color": "#ff8800", "marker-size": "medium", "marker-symbol": "star", "title": "Kitaga CBC" }, "geometry": { "type": "Point", "coordinates": [34.582, -0.955] } },
        { "type": "Feature", "properties": { "marker-color": "#ff0000", "marker-size": "medium", "marker-symbol": "star", "title": "Oyani CBC" }, "geometry": { "type": "Point", "coordinates": [34.568, -1.018] } },
        { "type": "Feature", "properties": { "marker-color": "#ff0000", "marker-size": "medium", "marker-symbol": "star", "title": "Goem CBC" }, "geometry": { "type": "Point", "coordinates": [34.625, -1.096] } },
        { "type": "Feature", "properties": { "marker-color": "#ff0000", "marker-size": "medium", "marker-symbol": "star", "title": "Ntoluo CBC" }, "geometry": { "type": "Point", "coordinates": [34.735, -1.115] } },
        { "type": "Feature", "properties": { "marker-color": "#ff0000", "marker-size": "medium", "marker-symbol": "star", "title": "Olalui CBC" }, "geometry": { "type": "Point", "coordinates": [34.845, -1.021] } },
        { "type": "Feature", "properties": { "marker-color": "#ff0000", "marker-size": "medium", "marker-symbol": "star", "title": "Factory Weighbridge" }, "geometry": { "type": "Point", "coordinates": [34.783, -1.334] } }
      ]
    };

    L.geoJSON(geojsonData, {
      pointToLayer: function (feature, latlng) {
        return L.marker(latlng, {
          icon: L.divIcon({
            className: 'custom-marker',
            html: '<div style="color: ' + feature.properties['marker-color'] + '">&#9733;</div>',
            iconSize: [20, 20]
          })
        }).bindPopup(feature.properties.title);
      }
    }).addTo(map);

    // Add heatmap
    var heatmapData = [
      [-0.955, 34.582, 0.5], [-0.96, 34.58, 0.5], [-0.95, 34.585, 0.5], [-0.95, 34.57, 0.5], [-0.96, 34.59, 0.5],
      [-0.94, 34.575, 0.5], [-0.93, 34.56, 0.5], [-0.92, 34.55, 0.5], [-0.91, 34.54, 0.5], [-0.9, 34.555, 0.5],
      [-0.89, 34.56, 0.5], [-0.88, 34.55, 0.5], [-0.87, 34.54, 0.5], [-0.86, 34.53, 0.5], [-0.85, 34.52, 0.5],
      [-0.84, 34.51, 0.5], [-0.83, 34.5, 0.5], [-0.82, 34.49, 0.5], [-0.81, 34.48, 0.5], [-0.8, 34.47, 0.5],
      [-0.79, 34.46, 0.5], [-0.78, 34.45, 0.5], [-0.77, 34.46, 0.5], [-0.76, 34.47, 0.5], [-0.75, 34.48, 0.5],
      [-0.74, 34.49, 0.5], [-0.73, 34.5, 0.5], [-0.74, 34.51, 0.5], [-0.75, 34.52, 0.5], [-0.76, 34.53, 0.5],
      [-0.85, 34.54, 0.5], [-0.86, 34.55, 0.5], [-0.87, 34.56, 0.5], [-0.88, 34.57, 0.5], [-0.89, 34.58, 0.5],
      [-0.9, 34.59, 0.5], [-0.91, 34.6, 0.5], [-0.92, 34.61, 0.5], [-0.93, 34.62, 0.5], [-0.94, 34.63, 0.5],
      [-0.95, 34.62, 0.5], [-0.96, 34.61, 0.5], [-0.97, 34.6, 0.5], [-0.98, 34.59, 0.5], [-0.99, 34.58, 0.5],
      [-1.0, 34.57, 0.5], [-1.01, 34.56, 0.5], [-1.02, 34.55, 0.5], [-1.03, 34.54, 0.5], [-1.04, 34.53, 0.5],
      [-1.05, 34.52, 0.5], [-1.06, 34.51, 0.5], [-1.07, 34.5, 0.5], [-1.08, 34.49, 0.5], [-1.09, 34.48, 0.5],
      [-1.1, 34.47, 0.5], [-0.98, 34.55, 0.5], [-0.99, 34.56, 0.5], [-1.0, 34.57, 0.5], [-1.01, 34.58, 0.5],
      [-1.02, 34.59, 0.5], [-1.03, 34.6, 0.5], [-0.814, 34.586, 0.2], [-0.82, 34.59, 0.2], [-0.81, 34.58, 0.2],
      [-0.8, 34.57, 0.2], [-0.83, 34.59, 0.2], [-0.825, 34.575, 0.2], [-1.096, 34.625, 0.2], [-1.1, 34.63, 0.2],
      [-1.09, 34.62, 0.2], [-1.08, 34.61, 0.2], [-1.11, 34.64, 0.2], [-1.334, 34.783, 0.2], [-1.34, 34.79, 0.2],
      [-1.33, 34.78, 0.2], [-1.32, 34.77, 0.2], [-1.35, 34.79, 0.2], [-1.34, 34.77, 0.2], [-1.36, 34.80, 0.2],
      [-1.115, 34.735, 0.2], [-1.12, 34.74, 0.2], [-1.11, 34.73, 0.2], [-1.1, 34.72, 0.2], [-1.13, 34.75, 0.2],
      [-1.021, 34.845, 0.2], [-1.03, 34.85, 0.2], [-1.02, 34.84, 0.2], [-1.01, 34.83, 0.2], [-1.04, 34.86, 0.2],
      [-0.8, 34.5, 0.3], [-0.79, 34.49, 0.3], [-0.78, 34.48, 0.3], [-0.77, 34.47, 0.3], [-0.76, 34.46, 0.3],
      [-0.75, 34.45, 0.3], [-0.74, 34.44, 0.3], [-0.73, 34.43, 0.3], [-0.72, 34.42, 0.3], [-0.71, 34.41, 0.3],
      [-0.7, 34.4, 0.3]
    ];

    L.heatLayer(heatmapData, {
      radius: 25,
      blur: 15,
      maxZoom: 12,
      gradient: { 0.4: 'blue', 0.65: 'lime', 1: 'red' }
    }).addTo(map);
  </script>
</body>
</html>
