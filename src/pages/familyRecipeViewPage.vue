<template>
  <div class="container">
    <div v-if="recipe">
      <div class="recipe-header mt-3 mb-4">
        <h1>{{ recipe.recipe_name }}</h1>
        <img :src="recipe.image_url" class="center" />
      </div>
      <div class="recipe-body">
        <div class="wrapper">
          <div class="wrapped">
            <div class="mb-3">
              <div><b>Create by</b> {{ recipe.author }} </div>
              <div><b>Ready in</b> {{ recipe.prep_time }} minutes</div>
              <div><b>Likes:</b> {{ recipe.aggregateLikes }} likes</div>
              <div><b>Cook for</b> {{ recipe.cook_for }} </div>
            </div>
            <b>Ingredients:</b>
            <ul>
              <li
                v-for="(r, index) in recipe.extendedIngredients"
                :key="index + '_' + r.id"
              >
                {{ r.original }}
              </li>
            </ul>
          </div>
          <div class="wrapped">
            <b>Instructions:</b>
            <ol>
              {{recipe.instructions}}
            </ol>
          </div>
        </div>
      </div>
      <!-- <pre>
      {{ $route.params }}
      {{ recipe }}
    </pre
      > -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      recipe: null
    };
  },
  async created() {
    try {
      // let response;
      // // response = this.$route.params.response;

      // try {
      //   response = await this.axios.get(
      //     "http://localhost:4000/users/displayMyRecipeInformation",       
      //     {
      //       params: { 
      //         recipe_id: this.$route.params.recipeId }
      //     }
      //   );

      //   // console.log("response.status", response.status);
      //   if (response.status !== 200) this.$router.replace("/NotFound");
      // } catch (error) {
      //   console.log("error.response.status", error.response.status);
      //   this.$router.replace("/NotFound");
      //   return;
      // }

      let {
        recipe_id,
        recipe_name,
        author,
        component,
        cook_for,
        prep_time,
        instructions,
	    vegan,
      	vegeterian,
      	gluten_free,
        aggregateLikes,
        image_url
                
      } = this.$route.params.recipe;//todo: ?

      // let _instructions = analyzedInstructions
      //   .map((fstep) => {
      //     fstep.steps[0].step = fstep.name + fstep.steps[0].step;
      //     return fstep.steps;
      //   })
      //   .reduce((a, b) => [...a, ...b], []);

      let _recipe = {
        recipe_id,
        recipe_name,
        author,
        component,
        cook_for,
        prep_time,
        instructions,
	    vegan,
      	vegeterian,
      	gluten_free,
        aggregateLikes,
        image_url 
      };

      this.recipe = _recipe;
    } catch (error) {
      console.log(error);
    }
  }
};
</script>

<style scoped>
.wrapper {
  display: flex;
}
.wrapped {
  width: 50%;
}
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
/* .recipe-header{

} */
</style>
