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

# Requête SQL et CartoCSS

    var subLayerOptions = {
      sql: "SELECT * FROM tableboutons where type = 'bornes'",
      cartocss: "#tableboutons{marker-fill: #109DCD; marker-width: 25; marker-line-color: white; marker-line-width: 5;}"
    }

# Boutons et requêtes SQL 

    <html>
    <head>
      <link rel="stylesheet" href="http://libs.cartocdn.com/cartodb.js/v3/3.11/themes/css/cartodb.css" />
      <script src="http://libs.cartocdn.com/cartodb.js/v3/3.11/cartodb.js"></script>
      <style>
        html, body {width:100%; height:100%; padding: 0; margin: 0;}
        #map { width: 100%; height:100%; background: black;}
        #menu { position: absolute; top: 5px; right: 100px; width: 400px; height:60px; background: transparent; z-index:10;}
        #menu a { 
          margin: 15px 10px 0 0;
          float: right;
          vertical-align: baseline;
          width: 70px;
          padding: 10px;
          text-align: center;
          font: bold 11px "Helvetica",Arial;
          line-height: normal;
          color: #555;
          border-radius: 4px;
          border: 1px solid #777777;
          background: #ffffff;
          text-decoration: none;
          cursor: pointer;
        }
        #menu a.selected,
        #menu a:hover { 
          color: #F84F40;
        }
      </style>
    
      <script>
      var map;
      function init(){
     // initiate leaflet map
        map = new L.Map('map', { 
        center: [48.10,-1.66],
        zoom: 13
        })
    
    // Fond de carte de base
    	
      L.tileLayer('http://a{s}.acetate.geoiq.com/tiles/acetate-hillshading/{z}/{x}/{y}.png', {attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'}).addTo(map);
    
      
    // Autres fonds de cartes
    
      
    var OSM = L.tileLayer('http://a{s}.acetate.geoiq.com/tiles/acetate-hillshading/{z}/{x}/{y}.png', {attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'});
        OpenStreetMap_HOT = L.tileLayer('http://{s}.tile.openstreetmap.fr/hot/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, Tiles courtesy of <a href="http://hot.openstreetmap.org/" target="_blank">Humanitarian OpenStreetMap Team</a>' });
         Esri_WorldImagery = L.tileLayer('http://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
    attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community' });
    
    var baseLayers = {"ESRI physical": OSM, 
                      "OSM Hot": OpenStreetMap_HOT,
                       "ESRI IMAG": Esri_WorldImagery };
      
    //Importation de la table CartoDB 
    var layerUrl = 'http://ninanoun.cartodb.com/api/v2/viz/50f50cb8-983a-11e4-bd4d-0e0c41326911/viz.json';
    
    // Configuration de la carte
    var sublayers = [];
    cartodb.createLayer(map, layerUrl).addTo(map)
      
     // Selecteur de couches 
    .on('done', function(lyr) {L.control.layers(baseLayers, { 'Donnees': lyr }).addTo(map);})
     
     // Configuration d'affichage des couches
     
    .on('done', function(layer) {
    var subLayerOptions = {
    sql: "SELECT * FROM tableboutons WHERE type = 'aaa'",
    cartocss: "#tableboutons{marker-fill: #F84F40; marker-width: 8; marker-line-color: white; marker-line-width: 2; marker-clip: false; marker-allow-overlap: true;}"
    }
    
    var sublayer = layer.getSubLayer(0);
    
    sublayer.set(subLayerOptions);
    
    sublayers.push(sublayer);
      }).on('error', function() {
      });
    
     // Parametrage des boutons (SQL et Carto CSS)
      
      
    var LayerActions = {
    
    Tout: function(){
    sublayers[0].set({
    sql: "SELECT * FROM tableboutons",
    cartocss: "#tableboutons{marker-fill: #FF9900; marker-width: 10; marker-line-color: white; marker-line-width: 0.5;}"
    });
    return true;
    },
    
    Velos: function(){
    sublayers[0].set({
    sql: "SELECT * FROM tableboutons WHERE type = 'velos'",
    cartocss: "#tableboutons{marker-fill: #109DCD; marker-width: 20; marker-line-color: white; marker-line-width: 1.5;}"
    });
    return true;
    },
    
    Bornes: function(){
    sublayers[0].set({
    sql: "SELECT * FROM tableboutons WHERE type = 'bornes'",
    cartocss: "#tableboutons{marker-fill: #FF9900; marker-width: 20; marker-line-color: white; marker-line-width: 1.5;}"
    });
    return true;
    },
    
    Recharge: function() {
    sublayers[0].set({
    sql: "SELECT * FROM tableboutons WHERE type = 'recharge'",
    cartocss: "#tableboutons{marker-fill: #B2DF8A; marker-width: 20; marker-line-color: white; marker-line-width: 1.5;}"
    });
    return true;
    },
    }
    
    
    $('.button').click(function() {
    $('.button').removeClass('selected');
    $(this).addClass('selected');
    //this gets the id of the different buttons and calls to LayerActions which responds according to the selected id
    LayerActions[$(this).attr('id')]();
    });
    
      
      }
      </script>
    </head>
    
    <body onload="init()">
      <div id='map'></div>
      <div id='menu'>
    <a href="#Recharge" id="Recharge" class="button Recharge">Recharge</a>
    <a href="#Velos" id="Velos" class="button Velos">Velos</a>
    <a href="#Bornes" id="Bornes" class="button Bornes">Bornes</a>
    <a href="#Tout" id="Tout" class="button Tout">Tout</a>
      </div>
    </body>
    </html>
