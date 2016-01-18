# CartoDB
Documentation pour CartoDB.js



# Cartes boutons 2016

<!DOCTYPE html>
<html>
    <head>
        <title>
            Lesson 3 | CartoDB.js | CartoDB
        </title>

        <meta name="viewport" content="initial-scale=1.0, user-scalable=no" />
        <meta http-equiv="content-type" content="text/html; charset=UTF-8" />

        <link rel="shortcut icon" href="http://cartodb.com/assets/favicon.ico" />

        <link rel="stylesheet" href="http://libs.cartocdn.com/cartodb.js/v3/3.15/themes/css/cartodb.css" type="text/css" />
        <link rel="stylesheet" href="http://academy.cartodb.com/css/cdbui.css" type="text/css" />

        <style type="text/css">
            html, body, #map {
                height: 100%;
                padding: 0;
                margin: 0;
            }
            #cartocss {
                position: absolute;
                top: 20px;
                right: 20px;
            }
            #sql {
                position: absolute;
                top: 20px;
                right: 292px;
            }
			  #titre {
                position: absolute;
                top: 20px;
                left: 200px;
            }
 
 .layer_selector2 {
                background: #FF4000;
                border-radius: 5px;
                padding: 0;
                border: 1px solid FE9A2E;
                width: 350px;
				color: #FFFFFF
            }
			            .layer_selector {
                background: rgba(255,255,255,0.9);
                border-radius: 5px;
                padding: 0;
                border: 1px solid #999;
                width: 250px;
            }
            
            .layer_selector > p {
                padding: 15px 30px;
                border-bottom: 1px solid #999;
            }
            
            .layer_selector ul {
                padding: 0; margin: 0;
                list-style-type: none;
            }
            .layer_selector li {
                padding: 15px 30px;
                font-family: Helvetica, Arial;
                font-size: 13px;
                color: #444;
                cursor: pointer;
            }
            .layer_selector li:not(:last-child) {
                border-bottom: 1px solid #999;
            }
            .layer_selector li:hover {
                background-color: #F0F0F0;
                cursor: pointer;
            }
            .layer_selector li.sql_selected,
            .layer_selector li.cartocss_selected {
                background-color: #A6CEE3;
            }
            </style>
           
            <style type="cartocss/html" id="simple">
                /** simple visualization */

                #all_day_cdb_gu_l3 {
                    marker-fill-opacity: 0.9;
                    marker-line-color: #FFF;
                    marker-line-width: 1.5;
                    marker-line-opacity: 1;
                    marker-placement: point;
                    marker-type: ellipse;
                    marker-width: 10;
                    marker-fill: #FF6600;
                    marker-allow-overlap: true;
                }
        </style>
        <style type="cartocss/html" id="quartier">
            /** category visualization */

#stations_le_velo_star_1 {
   marker-fill-opacity: 0.9;
   marker-line-color: #FFF;
   marker-line-width: 1;
   marker-line-opacity: 1;
   marker-placement: point;
   marker-type: ellipse;
   marker-width: 10;
   marker-allow-overlap: true;
}

#stations_le_velo_star_1[quartier="Bourg l'Evesque - La Touche - Moulin du Comte"] {
   marker-fill: #A6CEE3;
}
#stations_le_velo_star_1[quartier="Bréquigny"] {
   marker-fill: #1F78B4;
}
#stations_le_velo_star_1[quartier="Centre"] {
   marker-fill: #B2DF8A;
}
#stations_le_velo_star_1[quartier="Cleunay - Arsenal - Redon"] {
   marker-fill: #33A02C;
}
#stations_le_velo_star_1[quartier="Francisco-Ferrer - Vern - Poterie"] {
   marker-fill: #FB9A99;
}
#stations_le_velo_star_1[quartier="Jeanne d'Arc - Longs Champs - Atalante Beaulieu"] {
   marker-fill: #E31A1C;
}
#stations_le_velo_star_1[quartier="Maurepas - Patton"] {
   marker-fill: #FDBF6F;
}
#stations_le_velo_star_1[quartier="Sud gare"] {
   marker-fill: #FF7F00;
}
#stations_le_velo_star_1[quartier="Thabor - Saint-Hélier - Alphonse Guérin"] {
   marker-fill: #CAB2D6;
}
#stations_le_velo_star_1[quartier="Villejean - Beauregard"] {
   marker-fill: #6A3D9A;
}
#stations_le_velo_star_1 {
   marker-fill: #DDDDDD;
}
        </style>

        <style type="cartocss/html" id="Bubble">

#stations_le_velo_star_1{
  marker-fill-opacity: 0.9;
  marker-line-color: #FFF;
  marker-line-width: 1;
  marker-line-opacity: 1;
  marker-placement: point;
  marker-multi-policy: largest;
  marker-type: ellipse;
  marker-fill: #FF5C00;
  marker-allow-overlap: true;
  marker-clip: false;
}
#stations_le_velo_star_1 [ nb_socles <= 30] {
   marker-width: 35.0;
}
#stations_le_velo_star_1 [ nb_socles <= 28] {
   marker-width: 31.8;
}
#stations_le_velo_star_1 [ nb_socles <= 26] {
   marker-width: 28.6;
}
#stations_le_velo_star_1 [ nb_socles <= 25] {
   marker-width: 25.3;
}
#stations_le_velo_star_1 [ nb_socles <= 22] {
   marker-width: 22.1;
}
#stations_le_velo_star_1 [ nb_socles <= 20.5] {
   marker-width: 18.9;
}
#stations_le_velo_star_1 [ nb_socles <= 19] {
   marker-width: 15.7;
}
#stations_le_velo_star_1 [ nb_socles <= 16] {
   marker-width: 12.4;
}
#stations_le_velo_star_1 [ nb_socles <= 15] {
   marker-width: 9.2;
}
#stations_le_velo_star_1 [ nb_socles <= 12] {
   marker-width: 6.0;
}
        </style>

 <style type="cartocss/html" id="TPE">
#stations_le_velo_star_1 {
   marker-fill-opacity: 0.9;
   marker-line-color: #FFF;
   marker-line-width: 1;
   marker-line-opacity: 1;
   marker-placement: point;
   marker-type: ellipse;
   marker-width: 13;
   marker-allow-overlap: true;
}

#stations_le_velo_star_1[tpe="non"] {
   marker-fill: #FF2900;
}
#stations_le_velo_star_1[tpe="oui"] {
   marker-fill: #229A00;
}
 </style>

<style type="cartocss/html" id="metro">
            
#stations_le_velo_star_1 {
   marker-fill-opacity: 0.9;
   marker-line-color: #FFF;
   marker-line-width: 1;
   marker-line-opacity: 1;
   marker-placement: point;
   marker-type: ellipse;
   marker-width: 13;
   marker-allow-overlap: true;
}

#stations_le_velo_star_1[metro="non"] {
   marker-fill: #D6301D;
}
#stations_le_velo_star_1[metro="oui"] {
   marker-fill: #229A00;
}
        </style>
    </head>
    <body>
        <div id="map"></div>
        <div id="cartocss" class="layer_selector">
            <p><B>CartoCSS Selectors<B></p>
            <ul>
                <li data="quartier" data-type="cartocss">Catégorisation par quartier
                </li>
                <li data="Bubble" data-type="cartocss">Cercles proportionnels
                </li>
                <li data="TPE" data-type="cartocss">Equipée d'un TPE
                </li>
                <li data="metro" data-type="cartocss">A proximité d'un métro
                </li>
                <li data="simple" data-type="cartocss">Reset CartoCSS
                </li>
            </ul>
        </div>

        <div id="sql" class="layer_selector">
            <p><B>Sélecteur SQL<B></p>
            <ul>
                <li data=" WHERE nb_socles > 20" data-type="sql">Plus de 20 socles
                </li>
                <li data=" WHERE metro = 'oui'" data-type="sql">A proximité d'un métro
                </li>
                <li data=" WHERE tpe = 'oui'" data-type="sql">Equipée d'un terminal de paiement
                </li>
				<li data=" WHERE quartier='Centre'" data-type="sql">Quartier centre
                </li>
                <li data="" data-type="sql">Reset SQL</li>
            </ul>
        </div>
		
       <div id="titre" class="layer_selector2">
           <B><FONT size="10pt"><center>GéoDataViz.</center></FONT><B>       
        </div>
		
		
		
        <script src="http://libs.cartocdn.com/cartodb.js/v3/3.15/cartodb.js" type="text/javascript"></script>
        <script type="text/javascript">
        window.onload = function() {

      
            var tableName = "stations_le_velo_star_1";

            var layerSource = {
                    user_name: 'mastersigat',
                    type: 'cartodb',
                    sublayers: [{
                        sql: "SELECT * FROM " + tableName, 
                        cartocss: $("#simple").html() 
                    }]
            }
            
            var map_object = new L.Map('map', {
                center: [48.1098,-1.65], 
                zoom: 13
            });

            // Create layer selector
            function createSelector(layer) {
                var condition = "";
                var $options = $(".layer_selector").find("li");
                $options.click(function(e) {
                    var $li = $(e.target);
                    var selected = $li.attr('data');
                    var type = $li.data('type');

                    if (type === "cartocss") {
                        $options.removeClass('cartocss_selected');
                        if (selected !== "simple") {
                            $li.addClass('cartocss_selected');                      
                        }
                        condition = $('#'+selected).text();
                        layer.setCartoCSS(condition);
                    } else {
                        $options.removeClass('sql_selected');
                        if (selected !== "") {
                            $li.addClass('sql_selected');
                        }
                        layer.setSQL("SELECT * FROM " + tableName + selected);
                    }
                });
            }

            // Pull tiles from CartoDB's basemaps
            L.tileLayer('http://{s}.basemaps.cartocdn.com/dark_nolabels/{z}/{x}/{y}.png', {
                attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
            }).addTo(map_object);

            // for storing sublayer outside of createlayer
            var sublayers;

            // Add data layer to your map
            cartodb.createLayer(map_object,layerSource)
                .addTo(map_object)
                .done(function(layer) {
                    sublayer = layer.getSubLayer(0);
                    createSelector(sublayer);
                })
                .error(function(err) {
                    console.log("error: " + err);
                });
            }
        </script>
    </body>
</html>



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
