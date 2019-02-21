<template>
  <div class="recipes-new">
    <h1>New Recipe</h1>
    <div>
      Title: <input type="text" v-model="newRecipeTitle"><br>
      Ingredients: <input type="text" v-model="newRecipeIngredients"><br>
      Directions: <input type="text" v-model="newRecipeDirections"><br>
      Prep Time: <input type="text" v-model="newRecipePrepTime"><br>
      Image Url: <input type="text" v-model="newRecipeImageUrl"><br>

      <button v-on:click="createRecipe()">Create</button>
    </div>
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
      newRecipeImageUrl: ""
    };
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
        this.$router.push("/");
      });
    }
  }
};
</script>
