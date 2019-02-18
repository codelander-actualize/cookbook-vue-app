<template>
  <div class="home">

    <h1>{{ message }}</h1>

    <div v-for="recipe in recipes">
    	<h2>Title: {{ recipe.title }}</h2>
    	<p>Ingredients: {{ recipe.ingredients }}</p>
    	<p>Directions: {{ recipe.directions }}</p>
    	<p>Prep Time: {{ recipe.prep_time }}</p>
      <img :src="recipe.image_url" :alt="recipe.title">
    </div>

  </div>
</template>

<style>
  img {
    width: 300px;
  }
</style>

<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      message: "Hello World!",
      recipes: []
    };
  },
  created: function() {
  	axios.get("/api/recipes").then(response => {
  		this.recipes = response.data;
  	});
  },
  methods: {}
};
</script>

