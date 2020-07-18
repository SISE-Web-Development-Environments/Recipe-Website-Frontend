<template>
  <div class="container">
    <h1 class="title">search your recipe</h1>
    <b-row>
      <SearchRecipePreviewList title="search Recipes"/>
    </b-row>
  </div>
</template>
<script>
import SearchRecipePreviewList from '../components/SearchRecipePreviewList';
export default {
  components:{
    SearchRecipePreviewList
  }
};
</script>
