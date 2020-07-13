<template>
  <b-container>
    <h3>
      {{ title }}:
      <slot></slot>
    </h3>
    <b-row>
      <b-col v-for="r in recipes" :key="r.id">
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-col>
    </b-row>
  </b-container>
</template>
<script>
import RecipePreview from "./RecipePreview.vue";
export default {
    name: "SearchRecipePreviewList",
    components:{
        RecipePreview
    },
    props:{
        title:{
            type: String,
            required: true
        }

    },
    data(){
        return{
            recipes: []
        } 
    },
    mounted() {
        this.updateRecipe();
    },
    methods: {
       async updateRecipe(){
            try{
               const respone = await this.axios.get(
                   "http://localhost:4000/recipes/searchByTags?query=cheese&number=2&diet=true"
               );
               const recipes = respone.data;
               this.recipes = recipes;
            //    this.recipes = [];
            //    this.recipes.push(...recipes);
           }
           catch(error){
               console.log(error);
           }
       }
    }
};

</script>