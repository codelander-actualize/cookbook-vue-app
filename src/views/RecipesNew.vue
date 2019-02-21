<template>
  <div class="recipes-new">
    <h1>New Recipe</h1>

		<!-- <img v-if="status" v-bind:src="'https://http.cat/' + status" alt=""> -->
    <ul>
    	<li v-for="error in errors">{{ error }}</li>
    </ul>

    <form v-on:submit.prevent="submit()">
    	<div>
    	  Title: <input type="text" class="form-control" v-model="newRecipeTitle">
    	</div>
    	<div>
    		Ingredients: <input type="text" class="form-control" v-model="newRecipeIngredients">
    	</div>
    	<div>
    		Directions: <input type="text" class="form-control" v-model="newRecipeDirections">
    	</div>
    	<div>
    		Prep Time: <input type="text" class="form-control" v-model="newRecipePrepTime">
    	</div>
    	<div>
    		Image Url: <input type="text" class="form-control" v-model="newRecipeImageUrl">
    	</div>
			<div>
				<input type="submit" class="btn btn-primary" value="Create">
			</div>
    </form>

  </div>
</template>

<script>
import axios from 'axios';

export default {
  data: function() {
    return {
      newRecipeTitle: "",
      newRecipeIngredients: "",
      newRecipeDirections: "",
      newRecipePrepTime: "",
      newRecipeImageUrl: "",
      errors: [],
      // status: ""
    };
  },
  methods: {
    submit: function() {
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
        this.$router.push("/recipes/" + response.data.id);
      }).catch(error => {
      	this.errors = error.response.data.errors;
      	// this.status = error.response.status;
      });
    }
  }
};
</script>
