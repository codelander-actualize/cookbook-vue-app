<template>
  <div class="home">

    <h1>New Recipe</h1>
    <div>
      Title: <input type="text" v-model="newRecipeTitle"><br>
      Ingredients: <input type="text" v-model="newRecipeIngredients"><br>
      Directions: <input type="text" v-model="newRecipeDirections"><br>
      Prep Time: <input type="text" v-model="newRecipePrepTime"><br>
      Image Url: <input type="text" v-model="newRecipeImageUrl"><br>

      <button v-on:click="createRecipe()">Create</button>
    </div>

    <h1>All Recipes</h1>

    <div v-for="recipe in recipes">
    	<h2>Title: {{ recipe.title }}</h2>
      <img :src="recipe.image_url" :alt="recipe.title">
      <div>
        <button v-on:click="showRecipe(recipe)">More Info</button>
      </div>
      <div v-if="currentRecipe === recipe">
        <p>Ingredients: {{ currentRecipe.ingredients }}</p>
        <p>Directions: {{ currentRecipe.directions }}</p>
        <p>Prep Time: {{ currentRecipe.prep_time }}</p>
        <h4>Edit Recipe</h4>
        <div>
          Title: <input type="text" v-model="recipe.title"><br>
          Ingredients: <input type="text" v-model="recipe.ingredients"><br>
          Directions: <input type="text" v-model="recipe.directions"><br>
          Prep Time: <input type="text" v-model="recipe.prep_time"><br>
          Image Url: <input type="text" v-model="recipe.image_url"><br>
          <button v-on:click="updateRecipe(recipe)">Update</button>
        </div>
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
      newRecipeTitle: "",
      newRecipeIngredients: "",
      newRecipeDirections: "",
      newRecipePrepTime: "",
      newRecipeImageUrl: ""
    };
  },
  created: function() {
  	axios.get("/api/recipes").then(response => {
      console.log(response.data);
  		this.recipes = response.data;
  	});
  },
  methods: {
    createRecipe: function() {
      var recipeParams = {
        title: this.newRecipeTitle,
        ingredients: this.newRecipeIngredients,
        directions: this.newRecipeDirections,
        image_url: this.newRecipeImageUrl,
        prep_time: this.newRecipePrepTime,
        user_id: 1
      };
      axios.post("/api/recipes", recipeParams).then(response => {
        console.log("Success!", response.data);
        this.recipes.push(response.data);
      });
    },
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
    }
  }
};
</script>

