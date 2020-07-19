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
      <div v-bind:class="[seen ? 'recipe-seen' : '', 'recipe-footer']" >
        <div :title="recipe.title" class="recipe-title">{{ recipe.title }}</div>
        <ul class ="recipe-overview">
          <li><b>Ready in: {{ recipe.readyInMinutes }} minutes</b></li>
          <li><b>{{ recipe.aggregateLikes }} likes</b></li>
        </ul>
      </div>
    </router-link>
    <div class="recipe-indications">
      <b-button v-bind:class="[addedToFavorite ? 'recipe-is_favorite' : '', 'recipe-favorite']" @click="addToFavorites">
        <i id="heart" class="fa fa-heart"></i>
      </b-button>
      <b>    </b>
      <div v-if="vegeterian" id="vegetrian" class="indication">
         <i  class="fa fa-envira" aria-hidden="true"></i>
        <b>  Vegetarian  </b>
      </div>
      <div  v-if="vegan" id="vegan" class="indication">
        <i class="fa fa-tree" aria-hidden="true"></i>
        <b>  Vegan  </b>
      </div>
      <div  v-if="glutenFree" id="gluten" class="indication">
        <i class="fa fa-pagelines" aria-hidden="true"></i>
        <b>  Gluten Free  </b>
      </div>
     
      
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
      addedToFavorite: false,
      vegeterian: false,
      vegan: false,
      glutenFree: false
    };
  },
  mounted() {
    this.updateIsFavorite();
    this.updateIsSeen();
    this.checkIndications();
  },
  methods: {
    async updateIsFavorite() {
      try {
        const response = await this.axios.get(
          "http://localhost:4000/users/isFavorite",
          {
            params: {
              recipe_id: this.recipe.id
            }
          }
        );            
        this.addedToFavorite = response.data.answer;
      } catch (error) {
        console.log(error);
      }
    },

     async updateIsSeen() {
      try {
        const response = await this.axios.get(
          "http://localhost:4000/users/isSeen",
          {
            params: {
              recipe_id: this.recipe.id
            }
          }
        );            
        this.seen = response.data.answer;
      } catch (error) {
        console.log(error);
      }
    },

    async addToFavorites() {
      if (!this.addedToFavorite) {
        try {
          const response = await this.axios.post(
            "http://localhost:4000/users/addFavoriteRecipe",
            {
              recipe_id: this.recipe.id
            }            
          );
          this.addedToFavorite=true;
        } catch (error) {
          console.log(error);
        }
      }
    },
    async addToSeens() {
      
      if (!this.seen) {
        try {
          const response = await this.axios.post(
            "http://localhost:4000/users/addSeenRecipe",
            {
              recipe_id: this.recipe.id
            }
          );
        } catch (error) {
          console.log(error);
        }
      }
    },

    checkIndications(){
      this.vegeterian = this.recipe.vegetarian;
      this.vegan = this.recipe.vegan;
      this.glutenFree = this.recipe.glutenFree;
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

/* .recipe-preview .recipe-link:hover {
  color:saddlebrown
} */

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

.recipe-preview .recipe-link .recipe-body .recipe-image:hover {
border: 3px solid #42b983;
}

.recipe-preview .recipe-link .recipe-footer {
  width: 100%;
  height: 100%;
  overflow: hidden;  
}

.recipe-preview .recipe-link:hover {
  text-decoration: underline;
  text-decoration-color: rgb(35, 26, 163);  
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

.recipe-seen {
 color: rgb(146, 63, 184);  
  text-decoration-color: rgb(146, 63, 184);
}

.recipe-seen:hover {  
  text-decoration: underline;
  text-decoration-color: rgb(146, 63, 184); 
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
  text-decoration: bold;
}

.recipe-preview .recipe-indications .indication {
   display: inline;
   padding: 5px;  
}

.recipe-preview .recipe-indications .recipe-favorite {
  background-color: white;
}

.recipe-preview .recipe-indications .recipe-is_favorite {
  background-color: rgb(86, 155, 39);
}

#heart {
  color: rgb(111, 168, 106);
}

#heart:hover {
  color: rgb(17, 82, 9);
}
</style>
