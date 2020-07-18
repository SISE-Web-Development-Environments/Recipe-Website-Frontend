<template>
  <div class="container">
    <h1 class="title">My Recipes</h1>
    <b-row>
      <MyRecipePreviewList title=""/>
    </b-row>
  </div>
</template>
<script>
import MyRecipePreviewList from "../components/MyRecipePreviewList";
export default {
  components: {
    MyRecipePreviewList
  }
};
</script>