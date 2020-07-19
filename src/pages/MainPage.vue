<template>
  <div class="container">
    <h1 class="title">Main Page</h1>
    <b-row>
      <b-col>
        <RecipePreviewList title="Randome Recipes" request="random" class="RandomRecipes center" />
      </b-col>

      <b-col>
        <Login v-if="!$root.store.username" title="Login" />
        <!-- {{ !$root.store.username }} -->
        <RecipePreviewList
          v-else
          title="Last Viewed Recipes"
          request="seen"
          :class="{
          RandomRecipes: true,          
          center: true
        }"
          disabled
        ></RecipePreviewList>
      </b-col>
    </b-row>    
  </div>
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
import Login from "../components/Login";
export default {
  name: "MainPage",
  components: {
    RecipePreviewList,
    Login
  } 
};
</script>

<style lang="scss" scoped>
.RandomRecipes {
  margin: 10px 0 10px;
}


</style>
