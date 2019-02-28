<template>
  <div class="map">
    
    <div id='map'></div>

  </div>
</template>

<style>
  #map { 
    width: 700px; 
  }
  .mapboxgl-popup {
    max-width: 200px;
  }
</style>

<script>

export default {
  data: function() {
    return {
    };
  },
  mounted: function() {
    mapboxgl.accessToken = 'pk.eyJ1IjoiZHphZ2hpYW4iLCJhIjoiY2pzbnF0NmV0MGY2czQzbXBpMjcwMzRmNiJ9.Jei4-17Vu7hJSerisjPCEg';

    var marinis = [-122, 37]
    //create the map
    var map = new mapboxgl.Map({
    container: 'map', // container id
    style: 'mapbox://styles/mapbox/streets-v9', // stylesheet location
    center: marinis, // starting position [lng, lat]
    zoom: 10 // starting zoom
    });

    // create the popup
    var popup = new mapboxgl.Popup({ offset: 25 })
      .setText('This is my favorite ice cream in Santa Cruz');

    // create the marker
    var marker = new mapboxgl.Marker()
      .setLngLat(marinis)
      .setPopup(popup) // sets a popup on this marker
      .addTo(map);

  },
  methods: {}
};
</script>