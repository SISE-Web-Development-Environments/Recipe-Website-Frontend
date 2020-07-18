<template>
  <b-container>
    <h3>
      <slot></slot>
    </h3>
    <b-row>
      <b-col v-for="r in recipes" :key="r.id">
        <MyRecipePreview class="MyRecipePreview" :recipe="r" />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import MyRecipePreview from "./MyRecipePreview.vue";
export default {
  name: "MyRecipePreviewList",
  components: {
    MyRecipePreview
  },
  props: {
    title: {
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
    // console.log(this.$cookies.get("seesion"));
    this.updateRecipes();
  },
  methods: {
    async updateRecipes() {
      try {
        // var vm = this;
        // vm.loading = true;
        // var dataStr = 'username='+vm.username+'&password='+vm.password
        const response = await this.axios.get(
          "http://localhost:4000/users/getPersonalRecipes",{
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
