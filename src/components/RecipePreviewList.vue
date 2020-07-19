<template>
  <b-container>
    <h3>
      {{ title }}:
      <slot></slot>
    </h3>
    
      <b-row v-for="r in recipes" :key="r.id">
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-row>
    
  </b-container>
</template>

<script>
import RecipePreview from "./RecipePreview.vue";
export default {
  name: "RecipePreviewList",
  components: {
    RecipePreview
  },
  props: {
    title: {
      type: String,
      required: true
    },
    request:{
      type: String,
      required: true
    }
  },
  data() {
    return {
      recipes: []
    };
  },
  mounted() {
    this.updateRecipes();
  },
  methods: {
    async updateRecipes() {
      try {
        let x = this.request;
        let response = null;
        if(x=="random"){          
          response = await this.axios.get(
          "http://localhost:4000/recipes/getThreeRandomRecipes"          
          );
        }
        if(x=="seen"){          
          response = await this.axios.get(
          "http://localhost:4000/users/getLastThreeSeenRecipes"          
          );
        }
         if(x=="favorite"){          
          response = await this.axios.get(
          "http://localhost:4000/users/getFavoriteRecipes"          
          );
        }       
        
        const recipes = response.data.data;// instead of data.recipes
        this.recipes = [];
        this.recipes.push(...recipes);
        
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  min-height: 800px;
 
}
</style>
