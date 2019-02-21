<template>
  <div class="recipes-show">
    
    <h2>{{ recipe.title }}</h2>
    <p>Ingredients: {{ recipe.ingredients }}</p>
    <p>Directions: {{ recipe.directions }}</p>
    <p>Prep Time: {{ recipe.prep_time }}</p>

    <router-link to="/">Back to all recipes</router-link>

  </div>
</template>


<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      recipe: {}
    };
  },
  created: function() {
  	axios.get("/api/recipes/" + this.$route.params.id).then(response => {
      console.log(response.data);
  		this.recipe = response.data;
  	});
  },
  methods: {}
};
</script>