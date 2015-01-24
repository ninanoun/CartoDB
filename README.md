# CartoDB
Documentation pour CartoDB.js

# Première carte avec CartoDB

    <html>
    <head>
      <link rel="stylesheet" href="http://libs.cartocdn.com/cartodb.js/v3/themes/css/cartodb.css" />
      <script src="http://libs.cartocdn.com/cartodb.js/v3/cartodb.js"></script>
      <style>
        html, body {width:100%; height:100%; padding: 0; margin: 0;}
        #cartodb-map { width: 100%; height:100%; background: black;}
      </style>
    
      <script>
    
    // Appel de la carte et configuration 
      
    var map;
    function init(){
    map = new L.Map('cartodb-map', {
    center: [48.10,-1.66],
    zoom: 13})
    
    // Fond de carte
    
    L.tileLayer('http://a{s}.acetate.geoiq.com/tiles/acetate-hillshading/{z}/{x}/{y}.png', {attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'}).addTo(map);
    
    // Données issues de CartoDB
    
    var layerUrl = 'http://ninanoune.cartodb.com/api/v2/viz/bb28eda4-a3c3-11e4-b960-0e9d821ea90d/viz.json';
    
    // Options de chargement 
    cartodb.createLayer(map, layerUrl)
    .addTo(map)
    .on('done', function(layer) {
    }).on('error', function() {});
    }
    
      </script>
    </head>
    <body onload="init()">
      <div id='cartodb-map'></div>
    </body>
    </html>

# Fonds de cartes et sélecteur de couches


# Boutons et requêtes SQL 
