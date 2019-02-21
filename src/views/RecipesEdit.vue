<template>
  <div class="recipes-edit">

		<img v-if="status" v-bind:src="'https://http.cat/' + status" alt="">
    <ul>
    	<li v-for="error in errors">{{ error }}</li>
    </ul>

    <form v-on:submit.prevent="submit()">
    	<div>
    	  Title: <input type="text" class="form-control" v-model="recipe.title">
    	</div>
    	<div>
    		Ingredients: <input type="text" class="form-control" v-model="recipe.ingredients">
    	</div>
    	<div>
    		Directions: <input type="text" class="form-control" v-model="recipe.directions">
    	</div>
    	<div>
    		Prep Time: <input type="text" class="form-control" v-model="recipe.prep_time">
    	</div>
    	<div>
    		Image Url: <input type="text" class="form-control" v-model="recipe.image_url">
    	</div>
			<div>
				<input type="submit" class="btn btn-primary" value="Update">
			</div>
    </form>

  </div>
</template>

<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      recipe: {},
      errors: [],
      status: ""
    };
  },
  created: function() {
		axios.get("/api/recipes/" + this.$route.params.id).then(response => {
	    console.log(response.data);
			this.recipe = response.data;
  	});
  },
  methods: {
    submit: function() {
      var recipeParams = {
        title: this.recipe.title,
        ingredients: this.recipe.ingredients,
        directions: this.recipe.directions,
        image_url: this.recipe.image_url,
        prep_time: this.recipe.prep_time
      };
      axios.patch("/api/recipes/" + this.recipe.id, recipeParams).then(response => {
        console.log("Success!", response.data);
        this.$router.push("/recipes/" + this.recipe.id);
      }).catch(error => {
      	this.errors = error.response.data.errors;
      	this.status = error.response.status;
      });
    }
  }
};
</script>