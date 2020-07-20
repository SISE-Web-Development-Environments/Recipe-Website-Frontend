<template>
  <b-container>
    <h3>
      <slot></slot>
    </h3>
    <b-row>
       <b-row v-for="(group, i) in recipesGroups" :key="group" :list="i">
        <b-col v-for="recipe in recipes.slice(i * itemsPerRow, (i + 1) * itemsPerRow)" :key="recipe.id">
          <RecipePreview class="MyRecipePreview" :recipe="recipe" />
        </b-col>
      </b-row>
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
    }
  },
  data() {
    return {
      recipes: [],
      itemsPerRow: 2,
    };
  },
  mounted() {
    // console.log(this.$cookies.get("seesion"));
    this.updateRecipes();
  },
      computed: {
      recipesGroups () {
        return Array.from(Array(Math.ceil(this.recipes.length / this.itemsPerRow)).keys())
      }
  },
  methods: {
    async updateRecipes() {
      try {
        // var vm = this;
        // vm.loading = true;
        // var dataStr = 'username='+vm.username+'&password='+vm.password
        const response = await this.axios.get(
          "http://localhost:4000/users/getFavoriteRecipes",{
            // withCredentials: true
            params: {
              user_id: this.$root.store.user_id
            }
          }
        );

        // console.log(response);
        const recipes = response.data.data;
        this.recipes = [];
        this.recipes.push(...recipes);
        // console.log(this.recipes);
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  min-height: 400px;
}
</style>
