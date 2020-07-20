<template>
  <router-link :to="{ name: 'familyRecipe', params: { recipe: recipe }}" class="recipe-preview">
    <div class="recipe-body">
      <img :src="recipe.image_url" class="recipe-image" />
      <div class="text-over-image">
        <div class="text">
          <b>Watch Full Recipe</b>
        </div>
      </div>
    </div>
    <div class="recipe-footer">
      <div :title="recipe.recipe_name" class="recipe-title">
        <b>{{ recipe.recipe_name }}</b>
      </div>
      <ul class="recipe-overview">
        <li>{{ recipe.prep_time }} minutes</li>
        <li>{{ recipe.aggregateLikes }} likes</li>
        <li>{{ recipe.author }}</li>
      </ul>
    </div>
  </router-link>
</template>

<script>
export default {
  props: {
    recipe: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
.recipe-preview {
  display: block;
  width: 60%;
  height: 40%;
  position: relative;
}
.recipe-preview > .recipe-body {
  display: block;
  position: relative;
  margin: 10px 10px;
}

.recipe-preview .recipe-body .recipe-image {
  opacity: 1;
  margin-left: auto;
  margin-right: auto;
  margin-top: auto;
  margin-bottom: auto;
  display: block;
  width: 98%;
  height: auto;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  background-size: cover;
  transition: 0.5s ease;
  backface-visibility: hidden;
}

.recipe-preview .recipe-body:hover .recipe-image {
  opacity: 0.3;
}

.recipe-preview .recipe-body .text-over-image {
  opacity: 0;
  position: absolute;
  width: 100%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  text-align: center;
}

.recipe-preview .recipe-body:hover .text-over-image {
  opacity: 1;
}

.recipe-preview .recipe-body .text-over-image .text {
  color: rgb(12, 65, 33);
  font-size: 20px;
}

.recipe-preview .recipe-footer {
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.recipe-preview .recipe-footer .recipe-title {
  padding: 10px 10px;
  width: 100%;
  font-size: 12pt;
  text-align: left;
  white-space: nowrap;
  overflow: hidden;
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;
}

.recipe-preview .recipe-footer ul.recipe-overview {
  padding: 5px 10px;
  width: 100%;
  display: -webkit-box;
  display: -moz-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  box-flex: 1;
  -webkit-flex: 1 auto;
  -ms-flex: 1 auto;
  flex: 1 auto;
  table-layout: fixed;
  margin-bottom: 0px;
}

.recipe-preview .recipe-footer ul.recipe-overview li {
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  -ms-box-flex: 1;
  box-flex: 1;
  -webkit-flex-grow: 1;
  flex-grow: 1;
  width: 90px;
  display: table-cell;  
}
</style>
