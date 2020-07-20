<template>
<div>
    <b-container>
      <h3>
        {{ title }}:
        <slot></slot>
      </h3>      
        <b-row v-for="r in recipes" :key="r.id">            
          <RecipePreview class="recipePreview" :recipe="r"/>                
        </b-row>      
      </b-container>
    <br>
    <button v-if="isRandom" class="refresh" @click="refresh"> Refresh 3 Randoms Recipes </button>
</div>
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
      recipes: [],
      isRandom:false
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
          this.isRandom=true;        
          response = await this.axios.get(
          "http://localhost:4000/recipes/getThreeRandomRecipes"          
          );
        }
        if(x=="seen"){          
          response = await this.axios.get(
          "http://localhost:4000/users/getLastThreeSeenRecipes"          
          );
        }       
        
        const recipes = response.data.data;// instead of data.recipes
        this.recipes = [];
        this.recipes.push(...recipes);
        
      } catch (error) {
        console.log(error);
      }
    },
      refresh() {
      this.updateRecipes();
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  min-height: 800px;
 
}
.refresh {
  background-color: rgb(51, 131, 58);
  color: white;
  text-align: center;
  border: 3px solid green;
}
.refresh:hover{
   background-color: rgb(23, 71, 27);
}
</style>
