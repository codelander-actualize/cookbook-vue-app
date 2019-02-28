<template>
  <div class="map">
    
    <div id='map'></div>

  </div>
</template>

<style>
  #map { 
    width: inherit; 
    height: 900px;
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

    var places = [
      {
        lat: 37.974728,
        long: -122.03711,
        description: "Alpine Bakery in Concord, delicious pastries!"
      },
      {
        lat: 36.973804,
        long: -122.02575,
        description: "Marinis is my favorite ice cream in Santa Cruz"
      },
      {
        lat: 37.791852,
        long: -122.42127,
        description: "Bob's Donuts in SF makes gigantic donuts, good for sharing (or eating alone!)"
      }
    ]
    //create the map
    var map = new mapboxgl.Map({
      container: 'map', // container id
      style: 'mapbox://styles/mapbox/streets-v9', // stylesheet location
      center: [places[0].long, places[0].lat], // starting position [lng, lat]
      zoom: 8 // starting zoom
    });

    places.forEach(function(place){
      // create the popup
      var popup = new mapboxgl.Popup({ offset: 25 })
        .setText(place.description);
      // create the marker
      var marker = new mapboxgl.Marker()
        .setLngLat([place.long, place.lat])
        .setPopup(popup) // sets a popup on this marker
        .addTo(map);
    });

    map.addControl(new MapboxGeocoder({
      accessToken: mapboxgl.accessToken
    }));

  },
  methods: {}
};
</script>