<template>
  <div class="recipe-preview">
    <router-link
      :to="{ name: 'recipe', params: { recipeId: recipe.id } }"
      @click.native="addToSeens"
      class="recipe-link"
    >
      <div class="recipe-body">
        <img :src="recipe.image" class="recipe-image" />
      </div>
      <div class="recipe-footer">
        <div :title="recipe.title" class="recipe-title">{{ recipe.title }}</div>
        <ul class="recipe-overview">
          <li>{{ recipe.readyInMinutes }} minutes</li>
          <li>{{ recipe.aggregateLikes }} likes</li>
        </ul>
      </div>
    </router-link>
    <div class="recipe-indications">
      <b-button class="recipe-favorite" @click="addToFavorites">
        <i id="heart" class="fa fa-heart"></i>
      </b-button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    recipe: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      seen: false,
      addedToFavorite: false
    };
  },
  mounted() {
    
  },
  methods: {
    async addToFavorites() {
      if (!this.addedToFavorite) {
        try {
          response = await this.axios.post(
            "http://localhost:4000/users/addFavoriteRecipe",
            {
              recipe_id: this.recipe.id
            }
          );
        } catch (error) {
          console.log(error);
        }
      }
    },
    async addToSeens() {
      let x=3;
      if (!this.seen) {
        try {
          response = await this.axios.post(
            "http://localhost:4000/users/addSeenRecipe",
            {
              recipe_id: this.recipe.id
            }
          );
        } catch (error) {
          console.log(error);
        }
      }
    }
  }
};
</script>

<style scoped>
.recipe-preview {
  display: inline-block;
  position: relative;
  width: 60%;
  height: 40%;
  margin: 10px 10px;
}

.recipe-preview .recipe-link {
}

.recipe-preview .recipe-link .recipe-body {
  width: 100%;
  height: 80%;
  position: relative;
}

.recipe-preview .recipe-link .recipe-body .recipe-image {
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
}

.recipe-preview .recipe-link .recipe-footer {
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.recipe-preview .recipe-link .recipe-footer .recipe-title {
  padding: 10px 10px;
  width: 100%;
  font-size: 12pt;
  text-align: left;
  white-space: nowrap;
  overflow: hidden;
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;
}

.recipe-preview .recipe-link .recipe-footer ul.recipe-overview {
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

.recipe-preview .recipe-link .recipe-footer ul.recipe-overview li {
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  -ms-box-flex: 1;
  box-flex: 1;
  -webkit-flex-grow: 1;
  flex-grow: 1;
  width: 90px;
  display: table-cell;
  text-align: center;
}

.recipe-preview .recipe-indications {
}

.recipe-preview .recipe-indications .recipe-favorite {
  background-color: white;
}
#heart {
  color: rgb(110, 20, 20);
}

#heart:hover {
  color: rgb(226, 52, 52);
}
</style>
