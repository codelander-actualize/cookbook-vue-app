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
            <button class="btn btn-primary" v-on:click="setSortAttribute('title')">Sort by Title 
              <i class="icon-arrow-up" v-if="sortAttribute == 'title' && sortAscending == 1"></i>
              <i class="icon-arrow-down" v-if="sortAttribute == 'title' && sortAscending == -1"></i>
            </button>
            <button class="btn btn-primary" v-on:click="setSortAttribute('prep_time')">Sort by Prep Time
              <i class="icon-arrow-up" v-if="sortAttribute == 'prep_time' && sortAscending == 1"></i>
              <i class="icon-arrow-down" v-if="sortAttribute == 'prep_time' && sortAscending == -1"></i>
            </button>
          </div>


          <transition-group name="fade">
            <div v-for="recipe in orderBy(filterBy(recipes, titleFilter, 'title', 'ingredients'), sortAttribute, sortAscending)" class="col-md-4" v-bind:key="recipe.id">

              <router-link v-bind:to="'/recipes/' + recipe.id" class="item-grid text-center">
                <div class="image" :style="'background-image: url(' + recipe.image_url + ')'"></div>
                <div class="v-align">
                  <div class="v-align-middle">
                    <h3 class="title">{{ recipe.title }}</h3>
                    <h5 class="category">Preparation Time: {{ recipe.formatted.prep_time }}</h5>
                    <h5 class="category">Added: {{ relativeDate(recipe.created_at) }}</h5>
                  </div>
                </div>
              </router-link>
            </div>
          </transition-group>


        </div>
      </div>
    </div>

  </div>
</template>


<style>
  /* Vue.js fade */
  .fade-enter-active, .fade-leave-active {
    transition: opacity 1s
  }
  .fade-enter, .fade-leave-to {
    opacity: 0
  }

  /* Vue.js slide-right */
  .slide-right-enter-active {
    transition: all .3s ease;
  }
  .slide-right-leave-active {
    transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }
  .slide-right-enter, .slide-right-leave-to {
    transform: translateX(10px);
    opacity: 0;
  }

  /* Vue.js slide-left */
  .slide-left-enter-active {
    transition: all .3s ease;
  }
  .slide-left-leave-active {
    transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }
  .slide-left-enter, .slide-left-leave-to {
    transform: translateX(-10px);
    opacity: 0;
  }
</style>


<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";
import moment from "moment";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      recipes: [],
      currentRecipe: {},
      titleFilter: '',
      sortAttribute: 'title',
      sortAscending: 1
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
      if (this.sortAttribute === attribute) {
        this.sortAscending = this.sortAscending * -1;
      } else {
        this.sortAscending = 1;
      }
      this.sortAttribute = attribute;
    },
    relativeDate: function(date) {
      return moment(date).fromNow();
    }
  }
};
</script>

