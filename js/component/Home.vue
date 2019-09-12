<template>
  <div>
      <div v-if="homePage == 'allMusic'">
        <AllMusic></AllMusic>
        <button @click.prevent="changeHomePage('allFav')"> All Favorite </button>
      </div>
      <div v-else-if="homePage == 'allFav'">
        <AllFavorites></AllFavorites>
        <button @click.prevent="changeHomePage('allMusic')"> All Music </button>
      </div>
      <button @click.prevent='logout()'>Logout</button>
  </div>
</template>

<script>
import AllFavorites from './AllFavorites';
import AllMusic from './AllMusic'
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
        AllFavorites,
        AllMusic
    }
}
</script>

<style>
    
</style>