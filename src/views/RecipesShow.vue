<template>
  <div class="recipes-show">
    
    <h2>{{ recipe.title }}</h2>
    <img :src="recipe.image_url" :alt="recipe.title">
    <p>Ingredients: {{ recipe.ingredients }}</p>
    <p>Directions: {{ recipe.directions }}</p>
    <p>Prep Time: {{ recipe.prep_time }}</p>

    <router-link v-bind:to="'/recipes/' + recipe.id + '/edit'">Edit Recipe</router-link><br>

    <router-link to="/">Back to all recipes</router-link><br>

    <button v-on:click="destroyRecipe()">Destroy</button><br>

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
  methods: {
  	destroyRecipe: function() {
      axios.delete("/api/recipes/" + this.recipe.id).then(response => {
        console.log("Success!", response.data);
        this.$router.push("/")
      });
    }
  }
};
</script>