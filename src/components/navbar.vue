<template>
  <div>
      <!----------------Guest --------------------------->
    <span v-if="!$root.store.username">
        <b-navbar toggleable="lg" type="dark" variant="dark">
            <b-navbar-brand href='/main'>
                <p class="h3 mb-2"><b-icon icon="house-door-fill" style="color: #7952b3;"></b-icon></p>
            </b-navbar-brand>
                <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
            <b-collapse id="nav-collapse" is-nav>
                <b-navbar-nav>
                    <b-nav-item href="#" disabled> Hello Guest  </b-nav-item> 
                </b-navbar-nav>
                <b-navbar-nav>
                    <b-nav-item router-link :to="{ name: 'register' }"><b-icon icon="person-plus" style="color: #7952b3;"></b-icon>   Register  </b-nav-item>
                    <b-nav-item></b-nav-item>
                    <b-nav-item router-link :to="{ name: 'about' }"> About </b-nav-item>
                </b-navbar-nav>
                <b-navbar-nav class="ml-auto">
                    <b-nav-item router-link :to="{ name: 'search' }" >
                        <b-icon icon="search" style="color: #7952b3;"></b-icon> Search
                    </b-nav-item>
                    <b-nav-item ></b-nav-item>
                    <b-nav-item ></b-nav-item>
                <b-navbar-nav>
                    <b-nav-item ></b-nav-item>
                    <b-nav-item ></b-nav-item>
                </b-navbar-nav>
                    <b-nav-item router-link :to="{ name: 'login' }" ><b-icon icon="box-arrow-in-right" style="color: #7952b3;"></b-icon>   Login   </b-nav-item>
                </b-navbar-nav>

            </b-collapse>
        </b-navbar>
    </span>
    <!------------------- User ------------------------>
    <span v-else>
        <b-navbar toggleable="lg" type="dark" variant="dark">
            <b-navbar-brand href='/main'>
                <p class="h3 mb-2"><b-icon icon="house-door-fill" style="color: #7952b3;"></b-icon></p>
            </b-navbar-brand>
                <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
            <b-collapse id="nav-collapse" is-nav>
                <b-navbar-nav>
                    <b-nav-item href="#" disabled> Hello {{$root.store.username}}  </b-nav-item> 
                </b-navbar-nav>
                <b-navbar-nav>
                    <b-nav-item-dropdown right>
                        <template v-slot:button-content>
                            <em> {{$root.store.username}}</em>
                        </template>
                        <b-dropdown-item router-link :to="{ name: 'myFavourites' }"><b-icon icon="star-fill" style="color: #7952b3;"></b-icon>  Favorites</b-dropdown-item>
                        <b-dropdown-item router-link :to="{ name: 'myRecipes' }"><b-icon icon="receipt" style="color: #7952b3;"></b-icon>  My Recipe</b-dropdown-item>
                        <b-dropdown-item router-link :to="{ name: 'myFamilyRecipes' }"><b-icon icon="people-fill" style="color: #7952b3;"></b-icon>  Family Recipe</b-dropdown-item>
                    </b-nav-item-dropdown>
                    <b-nav-item></b-nav-item>
                    <b-nav-item>
                         <AddNewRecipe> Add New Recipe</AddNewRecipe>
                    </b-nav-item>
                    <b-nav-item></b-nav-item>
                    <b-nav-item router-link :to="{ name: 'about' }">About</b-nav-item>
                </b-navbar-nav>
                 <b-navbar-nav class="ml-auto">
                    <b-nav-item router-link :to="{ name: 'search' }" >
                        <b-icon icon="search" style="color: #7952b3;"></b-icon> Search
                    </b-nav-item>
                    <b-nav-item ></b-nav-item>
                    <b-nav-item ></b-nav-item>
                <b-navbar-nav>
                    <b-nav-item ></b-nav-item>
                    <b-nav-item ></b-nav-item>
                </b-navbar-nav>
                    <b-nav-item @click="Logout"><b-icon icon="box-arrow-left" style="color: #7952b3;"></b-icon>  Logout   </b-nav-item>
                </b-navbar-nav>
            </b-collapse>
        </b-navbar>
    </span>
    <!-- <b-nav-item href='/logout'><b-icon icon="box-arrow-left" style="color: #7952b3;"></b-icon>  logout   </b-nav-item> -->

  </div>
</template>

<script>
import Vue from 'vue'
import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'
import AddNewRecipe from '../AddNewRecipeModal'
Vue.use(BootstrapVue)
Vue.use(IconsPlugin)
// var user = this.$root.store.username
export default {
    components: {
        AddNewRecipe
    },
    methods: {
        Logout() {
        this.$root.store.logout();
        this.$root.toast("Logout", "User logged out successfully", "success");

        this.$router.push("/").catch(() => {
            this.$forceUpdate();
        });
        }
    }
}
</script>

<style>

</style>