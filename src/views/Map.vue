<template>
  <div class="map">
    
    <div id='map'></div>

  </div>
</template>

<style>
  #map { width: 700px; }
</style>

<script>

export default {
  data: function() {
    return {
    };
  },
  mounted: function() {
    mapboxgl.accessToken = 'pk.eyJ1IjoiZHphZ2hpYW4iLCJhIjoiY2pzbnF0NmV0MGY2czQzbXBpMjcwMzRmNiJ9.Jei4-17Vu7hJSerisjPCEg';
    var map = new mapboxgl.Map({
    container: 'map', // container id
    style: 'mapbox://styles/mapbox/streets-v9', // stylesheet location
    center: [-122.4, 37.7], // starting position [lng, lat]
    zoom: 10 // starting zoom
    });
  },
  methods: {}
};
</script>