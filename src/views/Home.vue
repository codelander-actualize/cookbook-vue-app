<template>
  <div class="home">

    <h1>All Recipes</h1>

    <div v-for="recipe in recipes">
    	<h2>Title: {{ recipe.title }}</h2>

      <router-link v-bind:to="'/recipes/' + recipe.id">
        <img :src="recipe.image_url" :alt="recipe.title">
      </router-link> 

      <div>
        <button v-on:click="showRecipe(recipe)">More Info</button>
      </div>
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
  methods: {
    showRecipe: function(recipe) {
      if (this.currentRecipe === recipe){
        this.currentRecipe = {};
      } else {
        this.currentRecipe = recipe;
      }
    },
    updateRecipe: function(recipe) {
      var recipeParams = {
        title: recipe.title,
        ingredients: recipe.ingredients,
        directions: recipe.directions,
        image_url: recipe.image_url,
        prep_time: recipe.prep_time
      };
      axios.patch("/api/recipes/" + recipe.id, recipeParams).then(response => {
        console.log("Success!", response.data);
        recipe = response.data;
      });
    },
    destroyRecipe: function(recipe) {
      axios.delete("/api/recipes/" + recipe.id).then(response => {
        console.log("Success!", response.data);
        // remove the destroyed recipe from the recipes array
        var index = this.recipes.indexOf(recipe);
        this.recipes.splice(index, 1);
      });
    }
  }
};
</script>

