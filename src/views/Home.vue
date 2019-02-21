<template>
  <div class="home">

    <h1>All Recipes</h1>

    <div v-for="recipe in recipes">
    	<h2>Title: {{ recipe.title }}</h2>

      <router-link v-bind:to="'/recipes/' + recipe.id">
        <img :src="recipe.image_url" :alt="recipe.title">
      </router-link> 

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
      recipes: [],
      currentRecipe: {},
    };
  },
  created: function() {
  	axios.get("/api/recipes").then(response => {
      console.log(response.data);
  		this.recipes = response.data;
  	});
  },
  methods: {}
};
</script>

