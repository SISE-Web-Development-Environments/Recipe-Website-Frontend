<template>
  <div class="container">
    <h1 class="title">Favorite Recipes</h1>
    <b-row>      
        <RecipePreviewList title="My Recipes" request="favorite" class="RandomRecipes center" />     
    </b-row>
  </div>
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
export default {
  name: "MyFavoriteRecipesPage",
  components: {
    RecipePreviewList    
  }
}
</script>

<style scoped>

</style>