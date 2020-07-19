 
<template>
  <div id="app">
    <div>
      <!----------------Guest --------------------------->
      <span v-if="!$root.store.username">
        <b-navbar toggleable="lg" type="dark" variant="dark">
          <b-navbar-brand href="/main">
            <!-- <router-link :to="{ name: 'main' }">Vue Recipes</router-link> -->
            <p class="h3 mb-2">
              <b-icon icon="house-door-fill" style="color: #6fa86a;"></b-icon>
            </p>
          </b-navbar-brand>
          <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
          <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
              <b-nav-item href="#" disabled>Hello Guest</b-nav-item>
            </b-navbar-nav>
            <b-navbar-nav>
              <b-nav-item router-link :to="{ name: 'register' }">
                <b-icon icon="person-plus" style="color: #6fa86a;"></b-icon>Register
              </b-nav-item>
              <b-nav-item></b-nav-item>
              <b-nav-item router-link :to="{ name: 'about' }">About</b-nav-item>
            </b-navbar-nav>
            <b-navbar-nav class="ml-auto">
              <b-nav-item router-link :to="{ name: 'search' }">
                <b-icon icon="search" style="color: #6fa86a;"></b-icon>Search
              </b-nav-item>
              <b-nav-item></b-nav-item>
              <b-nav-item></b-nav-item>
              <b-navbar-nav>
                <b-nav-item></b-nav-item>
                <b-nav-item></b-nav-item>
              </b-navbar-nav>
              <b-nav-item router-link :to="{ name: 'login' }">
                <b-icon icon="box-arrow-in-right" style="color: #6fa86a;"></b-icon>Login
              </b-nav-item>
            </b-navbar-nav>
          </b-collapse>
        </b-navbar>
      </span>
      <!------------------- User ------------------------>
      <span v-else>
        <b-navbar toggleable="lg" type="dark" variant="dark">
          <b-navbar-brand href="/main">
            <p class="h3 mb-2">
              <b-icon icon="house-door-fill" style="color: #6fa86a;"></b-icon>
            </p>
          </b-navbar-brand>
          <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
          <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
              <b-nav-item href="#" disabled>Hello {{$root.store.username}}</b-nav-item>
            </b-navbar-nav>
            <b-navbar-nav>
              <b-nav-item-dropdown right>
                <template v-slot:button-content>
                  <em>{{$root.store.username}}</em>
                </template>
                <!-- <b-dropdown-item router-link :to="{ name: 'myFavourites' }"><b-icon icon="star-fill" style="color: #7952b3;"></b-icon>  Favorites</b-dropdown-item> -->
                <!-- <b-dropdown-item router-link :to="{ name: 'myRecipe' }"><b-icon icon="receipt" style="color: #7952b3;"></b-icon>  My Recipe</b-dropdown-item> -->
                <b-dropdown-item router-link :to="{ name: 'myFavoriteRecipes' }">
                  <b-icon icon="heart" style="color: #6fa86a;"></b-icon>My Favorite Recipes
                </b-dropdown-item>
                <b-dropdown-item router-link :to="{ name: 'myRecipes' }">
                  <b-icon icon="receipt" style="color: #6fa86a;"></b-icon>My Recipes
                </b-dropdown-item>
                <b-dropdown-item router-link :to="{ name: 'myFamilyRecipes' }">
                  <b-icon icon="people-fill" style="color: #6fa86a;"></b-icon>My Family Recipes
                </b-dropdown-item>
                <!-- <b-dropdown-item router-link :to="{ name: 'familyRecipe' }"><b-icon icon="people-fill" style="color: #7952b3;"></b-icon>  Family Recipe</b-dropdown-item> -->
              </b-nav-item-dropdown>
              <b-nav-item router-link :to="{ name: 'about' }">About</b-nav-item>
            </b-navbar-nav>
            <b-navbar-nav class="ml-auto">
              <b-nav-item router-link :to="{ name: 'search' }">
                <b-icon icon="search" style="color: #6fa86a;"></b-icon>Search
              </b-nav-item>
              <b-nav-item></b-nav-item>
              <b-nav-item></b-nav-item>
              <b-navbar-nav>
                <b-nav-item></b-nav-item>
                <b-nav-item></b-nav-item>
              </b-navbar-nav>
              <b-nav-item @click="Logout">
                <b-icon icon="box-arrow-left" style="color: #6fa86a;"></b-icon>Logout
              </b-nav-item>
            </b-navbar-nav>
          </b-collapse>
        </b-navbar>
      </span>
      <!-- <b-nav-item href='/logout'><b-icon icon="box-arrow-left" style="color: #7952b3;"></b-icon>  logout   </b-nav-item> -->
    </div>
    <br>

    <router-view />
  </div>
</template>

<script>
import Vue from "vue";
import { BootstrapVue, IconsPlugin } from "bootstrap-vue";
Vue.use(BootstrapVue);
Vue.use(IconsPlugin);

export default {
  name: "App",

  methods: {
    async Logout() {
      try {
        console.log(this.$root.store.username);
        const response = await this.axios.post(
          "http://localhost:4000/auth/Logout"
        );
        console.log(response);
      } catch (err) {
        console.log(err.response);
      }
      this.$root.store.logout();
      localStorage.clear();
      this.$root.toast("Logout", "User logged out successfully", "success");
      this.$router.push("/").catch(() => {
        this.$forceUpdate();
      });
    }
  }
};
</script>

<style lang="scss">
@import "@/scss/form-style.scss";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
}
#nav {
  padding: 30px;
}
#nav a {
  font-weight: bold;
  color: #2c3e50;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

