<template>
  <div class="container">
    <h1 class="title">search your recipe</h1>
    <b-col>
      <SearchRecipePreviewList title="search Recipes"/>
    </b-col>
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
