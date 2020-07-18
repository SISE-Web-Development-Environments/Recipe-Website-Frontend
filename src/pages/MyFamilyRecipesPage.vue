<template>
  <div class="container">
    <h1 class="title">My Family Recipes</h1>
    <b-row>
      <MyFamilyRecipePreviewList title=""/>
    </b-row>
  </div>
</template>
<script>
import MyFamilyRecipePreviewList from "../components/MyFamilyRecipePreviewList";
export default {
  components: {
    MyFamilyRecipePreviewList
  }
};
</script>