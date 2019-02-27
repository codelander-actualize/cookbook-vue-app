<template>
  <div class="recipes-index">

    <div id="fh5co-work-section">
      <div class="container">
        <div class="row">

          
          <div>
            Search by Title: <input type="text" class="form-control" v-model="titleFilter" list="recipeTitles">
          </div><br>

          <datalist id="recipeTitles">
            <option v-for="recipe in recipes">{{ recipe.title }}</option>
          </datalist>

          <div>
            <button class="btn btn-primary" v-on:click="setSortAttribute('title')">Sort by Title</button>
            <button class="btn btn-primary" v-on:click="setSortAttribute('prep_time')">Sort by Prep Time</button>
          </div>

          <div v-for="recipe in orderBy(filterBy(recipes, titleFilter, 'title', 'ingredients'), sortAttribute)" class="col-md-4">

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


<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      recipes: [],
      currentRecipe: {},
      titleFilter: '',
      sortAttribute: 'title'
    };
  },
  created: function() {
  	axios.get("/api/recipes").then(response => {
      console.log(response.data);
  		this.recipes = response.data;
  	});
  },
  methods: {
    setSortAttribute: function(attribute) {
      this.sortAttribute = attribute;
    }
  }
};
</script>

