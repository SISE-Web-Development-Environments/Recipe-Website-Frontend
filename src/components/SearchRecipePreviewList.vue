<template>
  <b-container>
    <h3>
      <slot></slot>
    </h3>
    <b-form @submit.prevent="onSearch">
      <b-form-group
        id="input-group-name"
        label-for="name"
      >
        <b-form-input
          id="name"
          v-model="$v.form.name.$model"
          type="text"
          placeholder="name of recipe"
          :state="validateState('name')"
        ></b-form-input>
        <b-form-invalid-feedback>name is required</b-form-invalid-feedback>
      </b-form-group>
       <b-form-group
        id="input-group-cuisine"
        label-for="cuisine"
      >
        <b-form-select
          id="cuisine"
          v-model="$v.form.cuisine.$model"
          :options="cuisines"
        ></b-form-select>
      </b-form-group>
      <b-form-group
        id="input-group-diet"
        label-for="diet"
      >
        <b-form-select
          id="diet"
          v-model="$v.form.diet.$model"
          :options="diets"
        ></b-form-select>
      </b-form-group>
      <b-form-group
        id="input-group-intolerances"
        label-for="intolerances"
      >
        <b-form-select
          id="intolerances"
          v-model="$v.form.intolerances.$model"
          :options="intolerances"
        ></b-form-select>
      </b-form-group>
      <b-form-group
        id="input-group-numbers"
        label-cols-sm="3"
        label="number of results:"
        label-for="numbers"
      >
        <b-form-select
          id="numbers"
          v-model="$v.form.number.$model"
          :options="numbers"
        ></b-form-select>
      </b-form-group>
     <b-button
        type="submit"
        variant="primary"
        style="width:100px;display:block;"
        class="mx-auto w-100"
      >search</b-button>
    </b-form>

    <b-form-group
        id="input-group-sort"
        label-for="sort"
      >
        <b-form-select
          id="sort"
          v-model="sortby_selected"
          @change="sortby"
           :disabled="!recipes || !recipes.length"
          >
          <b-form-select-option :value="null" disabled
              >sort by</b-form-select-option
            >
            <b-form-select-option value="time"
              >sort by time</b-form-select-option
            >
            <b-form-select-option value="like"
              >sort by popular</b-form-select-option
            >
        </b-form-select>
      </b-form-group>

    <b-row>
      <b-col v-for="r in recipes" :key="r.id">
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-col>
    </b-row>
    <b-row v-if="searchEmpty" class="empty">
        No search results :(
    </b-row>
  </b-container>
</template>
<script>
import RecipePreview from "./RecipePreview.vue";
import cuisines from "../assets/cuisines";
import diets from "../assets/diet";
import numbers from "../assets/numbers";
import intolerances from "../assets/intolerances";
import { required } from "vuelidate/lib/validators";
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
            recipes: [],
            form: {
              name: "",
              cuisine: null,
              diet: null,
              intolerances: null,
              number: 5
            },
            diets: [{ value: null, text: "filtering by diet", disabled: true }],
            cuisines: [{ value: null, text: "filtering by cusine", disabled: true }],
            numbers: [{ value: null, text: "", disabled: true }],
            intolerances: [{ value: null, text: "filtering by intolerances", disabled: true }],
            sortby_selected: null,
            searchEmpty: false,
        }; 
    },
    mounted() {
    this.cuisines.push(...cuisines);
    this.diets.push(...diets);
    this.numbers.push(...numbers);
    this.intolerances.push(...intolerances);
     if (this.$root.store.username) {
       if (localStorage.search){
         let search_history = JSON.parse(localStorage.search);
         this.form.name = search_history.name;
         this.form.cuisine = search_history.cuisine;
         this.form.diet = search_history.diet;
         this.form.intolerances = search_history.intolerances;
         this.form.number = search_history.number;
         this.form.searchEmpty = search_history.searchEmpty;
         this.recipes = search_history.recipes;
       }
     }
    
  },
    validations: {
    form: {
      name: {
        required
      },
      cuisine:{
      },
      diet:{

      },
      number: {

      },
      intolerances:{

      },
    },
  },
    methods: {
      validateState(param) {
      const { $dirty, $error } = this.$v.form[param];
      return $dirty ? !$error : null;
      },
      async updateSearchResultsRecipes(){
            try{

              
              const response = await this.axios.get(
                  // "http://localhost:4000/recipes/searchByTags?query=cheese&number=2&diet=true"
                  "http://localhost:4000/recipes/searchByTags", {
                    params: {
                      query: this.form.name,
                      cuisine: this.form.cuisine,
                      diet: this.form.diet,
                      intolerances: this.form.intolerances,
                      number: this.form.number
                    }
                  }
              );
              
              const recipes = response.data.data;// instead of data.recipes
              this.recipes = [];
              this.recipes.push(...recipes);
            
              if (this.recipes.length == 0) {
                 this.searchEmpty = true;
              }
              if (this.$root.store.username) {
                let search_history = new Object();
                search_history.name = this.form.name;
                search_history.cuisine = this.form.cuisine;
                search_history.diet = this.form.diet;
                search_history.intolerances = this.form.intolerances;
                search_history.number = this.form.number;
                search_history.searchEmpty = this.searchEmpty;
                search_history.recipes = this.recipes;
                localStorage.search = JSON.stringify(search_history);
              }
            }
            catch(error){
               console.log(error);
            }
       },
       onSearch() {
        // console.log("login method called");
        this.form.submitError = undefined;
        this.$v.form.$touch();
        if (this.$v.form.$anyError) {
          return;
        }
        // console.log("login method go");

        this.updateSearchResultsRecipes();
      },
      sortby() {
      if (this.sortby_selected == "time") {
        function compareTime(a, b) {
          if (a.readyInMinutes < b.readyInMinutes) return -1;
          if (a.readyInMinutes > b.readyInMinutes) return 1;
          return 0;
        }
        return this.recipes.sort(compareTime);
      } else if (this.sortby_selected == "like") {
        function compareLikes(a, b) {
          if (a.aggregateLikes < b.aggregateLikes) return 1;
          if (a.aggregateLikes > b.aggregateLikes) return -1;
          return 0;
        }
        return this.recipes.sort(compareLikes);
      } 
        return this.recipes.sort(readyInMinutes);
      }
    }
};

</script>
<style scoped>
.empty {
  font-size: 24px;
  padding: 30px;
}
</style>