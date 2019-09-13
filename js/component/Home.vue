<template>
  <div>
      <!-- <div v-if="homePage == 'allMusic'">
        <AllMusic></AllMusic>
        <button @click.prevent="changeHomePage('allFav')"> All Favorite </button>
      </div>
      <div v-else-if="homePage == 'allFav'">
        <AllFavorite></AllFavorite>
        <button @click.prevent="changeHomePage('allMusic')"> All Music </button>
      </div> -->
      <Navbar @logout="logout()"></Navbar>
      <Main :homePage="homePage">
          
      </Main>
  </div>
</template>

<script>
import Navbar from './Navbar'
import Main from './Main'
import AllFavorite from './AllFavorite'
import AllMusic from './AllMusic'


export default {
    data : function(){
        return {
            homePage : "allMusic"
        }
    },
    methods : {
        logout() {
            console.log('home')
            localStorage.removeItem('token');
            this.$emit('logout');
        },
        changeHomePage( page ) {
            this.homePage = page;
        }
    },
    components : {
        AllFavorite,
        AllMusic,
        Navbar,
        Main
    }
}
</script>

<style>
    
</style>