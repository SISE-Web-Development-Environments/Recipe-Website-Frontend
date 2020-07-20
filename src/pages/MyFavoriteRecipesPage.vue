<template>
  <div class="container">
    <h1 class="title">Favorite Recipes</h1>
    <b-row>      
        <FavoriteRecipePreviewList title="My Recipes" request="favorite" class="RandomRecipes center" />     
    </b-row>
  </div>
</template>

<script>
import FavoriteRecipePreviewList from "../components/FavoriteRecipePreviewList";
export default {
  name: "MyFavoriteRecipesPage",
  components: {
    FavoriteRecipePreviewList    
  }
}
</script>

<style  lang="scss" scoped>
</style>