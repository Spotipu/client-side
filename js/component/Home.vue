<template>
  <div>
<<<<<<< HEAD
      <!-- <div v-if="homePage == 'allMusic'">
        <AllMusic></AllMusic>
        <button @click.prevent="changeHomePage('allFav')"> All Favorite </button>
      </div>
      <div v-else-if="homePage == 'allFav'">
        <AllFavorites></AllFavorites>
        <button @click.prevent="changeHomePage('allMusic')"> All Music </button>
      </div> -->
      <Navbar @logout="logout()"></Navbar>
      <Main :homePage="homePage"></Main>
=======
      <div v-if="homePage == 'allMusic'">
            <AllMusic></AllMusic>
            <button @click.prevent="changeHomePage('allFav')"> All Favorite </button>
            <button @click.prevent="changeHomePage('myMusic')"> My Music</button>

      </div>
      <div v-else-if="homePage == 'allFav'">
            <AllFavorite></AllFavorite>
            <button @click.prevent="changeHomePage('allMusic')"> All Music </button>
            <button @click.prevent="changeHomePage('myMusic')"> My Music</button>

      </div>
      <div v-else-if="homePage == 'myMusic'">
            <MyMusic></MyMusic>
            <button @click.prevent="changeHomePage('allMusic')"> All Music</button>
            <button @click.prevent="changeHomePage('allFav')"> All Favorite </button>
      </div>
      <button @click.prevent='logout()'>Logout</button>
>>>>>>> cb5303131a90ffb8034348eaab3b14eb5887215f
  </div>
</template>

<script>
<<<<<<< HEAD
import Navbar from './Navbar'
import Main from './Main'

import AllFavorites from './AllFavorites'
import AllMusic from './AllMusic'

=======
import AllFavorite from './AllFavorite';
import AllMusic from './AllMusic'
import MyMusic from './MyMusic'
>>>>>>> cb5303131a90ffb8034348eaab3b14eb5887215f

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
<<<<<<< HEAD
        AllFavorites,
        AllMusic,
        Navbar,
        Main
=======
        AllFavorite,
        AllMusic,
        MyMusic
>>>>>>> cb5303131a90ffb8034348eaab3b14eb5887215f
    }
}
</script>

<style>
    
</style>