<template>
  <div class="home">

    <h1>New Recipe</h1>
    <button v-on:click="createRecipe()">Create</button>
    <h1>All Recipes</h1>

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
      recipes: []
    };
  },
  created: function() {
  	axios.get("/api/recipes").then(response => {
  		this.recipes = response.data;
  	});
  },
  methods: {
    createRecipe: function() {
      var recipeParams = {
        title: "Veggie Lasagna",
        ingredients: "Noodles, sauce, vegetables, spices",
        directions: "Layer carefully into a dish and bake",
        image_url:"https://cdn-image.myrecipes.com/sites/default/files/styles/medium_2x/public/image/recipes/sl/11/02/fresh-vegetable-lasagna-sl-x.jpg?itok=Uu1Gar28",
        prep_time: 150,
        user_id: 1
      };
      axios.post("/api/recipes", recipeParams).then(response => {
        console.log("Success!", response.data);
        this.recipes.push(response.data);
      });
    }
  }
};
</script>

