<template>
  <div class="recipes-index">

    <div id="fh5co-work-section">
      <div class="container">
        <div class="row">

          
          <div>
            Search by Title: <input type="text" class="form-control" v-model="titleFilter">
          </div>
          <div v-for="recipe in filterBy(recipes, titleFilter, 'title', 'ingredients')" class="col-md-4">
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
      titleFilter: ''
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

