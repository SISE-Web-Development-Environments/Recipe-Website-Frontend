<template>
  <div class="container">
    <h1 class="title">Main Page</h1>
    <b-row>
      <b-col>
        <RecipePreviewList title="Randome Recipes" class="RandomRecipes center" />
      </b-col>
      <b-col>
        <!-- <router-link
          v-if="!$root.store.username"
          to="/login"
          tag="button"
        >You need to Login to vue this</router-link>-->
        <Login v-if="!$root.store.username" title="Login" />
        <!-- {{ !$root.store.username }} -->
        <RecipePreviewList
          v-else
          title="Last Viewed Recipes"
          :class="{
          RandomRecipes: true,
          blur: !$root.store.username,
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
.blur {
  -webkit-filter: blur(5px); /* Safari 6.0 - 9.0 */
  filter: blur(2px);
}
::v-deep .blur .recipe-preview {
  pointer-events: none;
  cursor: default;
}
</style>
