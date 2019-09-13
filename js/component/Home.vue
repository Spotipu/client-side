<template>
  <div>
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
  </div>
</template>

<script>
import AllFavorite from './AllFavorite';
import AllMusic from './AllMusic'
import MyMusic from './MyMusic'

export default {
    data : function(){
        return {
            homePage : "allMusic"
        }
    },
    methods : {
        logout() {
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
        MyMusic
    }
}
</script>

<style>
    
</style>