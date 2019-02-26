<template>
  <div class="recipes-index">

    <div id="fh5co-work-section">
      <div class="container">
        <div class="row">


          <div v-for="recipe in recipes" class="col-md-4">
            <router-link v-bind:to="'/recipes/' + recipe.id" class="item-grid text-center">
              <div class="image" :style="'background-image: url(' + recipe.image_url + ')'"></div>
              <div class="v-align">
                <div class="v-align-middle">
                  <h3 class="title">{{ recipe.title }}</h3>
                  <h5 class="category">Preparation Time: {{ recipe.formatted.prep_time }}</h5>
                </div>
              </div>
            </router-link>
          </div>


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

