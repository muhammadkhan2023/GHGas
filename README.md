<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ArcGIS Web App with WebScene</title>
  <link rel="stylesheet" href="https://js.arcgis.com/4.27/esri/themes/light/main.css">
  <script src="https://js.arcgis.com/4.27/"></script>
  <style>
    html, body, #viewDiv {
      height: 100%;
      margin: 0;
      padding: 0;
    }
  </style>
</head>
<body>
  <div id="viewDiv"></div>
  <script>
    require([
      "esri/WebScene",
      "esri/views/SceneView",
      "esri/widgets/Search"
    ], function(WebScene, SceneView, Search) {

      // Load your WebScene by its ID
      const webscene = new WebScene({
        portalItem: {
          id: "8362167f419340b59a0162c93a0ed961"  // Replace with your WebScene ID
        }
      });

      const view = new SceneView({
        container: "viewDiv",
        map: webscene,
        zoom: 2
      });

      // Add a Search widget
      const searchWidget = new Search({
        view: view
      });

      view.ui.add(searchWidget, "top-right");

      // Add a click event listener
      view.on("click", function(evt){
        var vLat=evt.mapPoint.latitude;
        var vLon=evt.mapPoint.longitude;
        var heading=view.camera.heading;
        console.log("scene clicked at", evt.mapPoint);
        var gUrl = 'https://www.google.com/maps/@?api=1&map_action=pano&viewpoint=${vLat},${vLon}&heading=${heading}';
        window.open(gUrl, "StreetView","width=800,height=600");
      
      });
    });
  </script>
</body>
</html>
