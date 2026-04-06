<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Map</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
        integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY=" crossorigin="" />
    <!-- Make sure you put this AFTER Leaflet's CSS -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"
        integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo=" crossorigin=""></script>
</head>
<body>
    <div id="map"></div>
</body>
<style>
    #map {
        height: 650px;
        width: 650px;
    }

    /* Leaflet crispness override */
    .leaflet-container .leaflet-overlay-pane svg,
    .leaflet-container .leaflet-marker-pane img,
    .leaflet-container .leaflet-shadow-pane img,
    .leaflet-container .leaflet-tile-pane img,
    .leaflet-container img.leaflet-image-layer {
        max-width: none !important;
        /* Preserve crisp pixels with scaled up images */
        image-rendering: optimizeSpeed;
        /* Legal fallback */
        image-rendering: -moz-crisp-edges;
        /* Firefox        */
        image-rendering: -o-crisp-edges;
        /* Opera          */
        image-rendering: -webkit-optimize-contrast;
        /* Safari         */
        image-rendering: optimize-contrast;
        /* CSS3 Proposed  */
        image-rendering: crisp-edges;
        /* CSS4 Proposed  */
        image-rendering: pixelated;
        /* CSS4 Proposed  */
        -ms-interpolation-mode: nearest-neighbor;
        /* IE8+           */
    }

    .leaflet-container {
        background-color: rgb(32, 32, 32);
    }
</style>
<script>
    var map = L.map('map', {
        crs: L.CRS.Simple
    });
    const bounds = L.latLngBounds(
        [0, 0],
        [464, 768]
    );
    var image = L.imageOverlay('assets/map.png', bounds).addTo(map);
    map.fitBounds(bounds);
    const padded = bounds.pad(0.1)
    map.setMaxBounds(padded)
    map.setView([{{ include.lat | default: "300" }}, {{ include.long | default: "350" }}], 2);
    var popup = L.popup();

    function onMapClick(e) {
        popup
            .setLatLng(e.latlng)
            .setContent("You clicked the map at " + e.latlng.toString())
            .openOn(map);
    }

    map.on('click', onMapClick);
</script>

</html>