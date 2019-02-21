<template>
  <div class="recipes-index">

    <h1>All Recipes</h1>

    <div class="card-columns">
      <div v-for="recipe in recipes">
        
        <router-link v-bind:to="'/recipes/' + recipe.id">
          <div class="card" style="width: 18rem;">
            <img :src="recipe.image_url" class="card-img-top" :alt="recipe.title">
            <div class="card-body">
              <p class="card-text">{{ recipe.title }}</p>
            </div>
          </div>
        </router-link>

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
  methods: {}
};
</script>

