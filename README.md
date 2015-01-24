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

    <html>
    <head>
      <link rel="stylesheet" href="http://libs.cartocdn.com/cartodb.js/v3/themes/css/cartodb.css" />
      <script src="http://libs.cartocdn.com/cartodb.js/v3/cartodb.js"></script>
      <style>
        html, body {width:100%; height:100%; padding: 0; margin: 0;}
        #cartodb-map { width: 100%; height:100%; background: black;}
      </style>
    
      <script>
      
    // Initialisation de la carte 
    
    var map;
    function init(){
    map = new L.Map('cartodb-map', {
    center: [48.11,-1.66],
    zoom: 13})
      
      //fond de carte de base
    
    L.tileLayer('http://a{s}.acetate.geoiq.com/tiles/acetate-hillshading/{z}/{x}/{y}.png', {attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'}).addTo(map);
      
      // Autres fonds de carte
        
    var OSM = L.tileLayer('http://a{s}.acetate.geoiq.com/tiles/acetate-hillshading/{z}/{x}/{y}.png', {attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'});
        OpenStreetMap_HOT = L.tileLayer('http://{s}.tile.openstreetmap.fr/hot/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, Tiles courtesy of <a href="http://hot.openstreetmap.org/" target="_blank">Humanitarian OpenStreetMap Team</a>' });
         Esri_WorldImagery = L.tileLayer('http://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
    attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community' });
    
    var baseLayers = {"ESRI physical": OSM, 
                      "OSM Hot": OpenStreetMap_HOT,
                      "ESRI IMAG": Esri_WorldImagery };
       
      //Ajout des donnees CartoDB
      
      var layerUrl = 'http://ninanoun.cartodb.com/api/v2/viz/50f50cb8-983a-11e4-bd4d-0e0c41326911/viz.json';
    
        // Selecteur de fond de carte
    
    cartodb.createLayer(map, layerUrl).addTo(map)
    .on('done', function(lyr) {L.control.layers(baseLayers, { 'Donnees': lyr }).addTo(map);})
    .on('done', function(layer) {
    layer.getSubLayer(0).set(subLayerOptions);
    }).on('error', function() {});
    }
      </script>
    </head>
    <body onload="init()">
      <div id='cartodb-map'></div>
    </body>
    </html>

# Boutons et requêtes SQL 
