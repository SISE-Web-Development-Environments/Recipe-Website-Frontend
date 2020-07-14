<template>
  <div class="container">
    <h1 class="title">My Recipes Page</h1>
    <MyRecipePreviewList title=""/>
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