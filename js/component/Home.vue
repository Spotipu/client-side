<template>
  <div>
      <div v-if="homePage == 'allMusic'">
        <AllMusic :allMusic='allMusic'></AllMusic>
        <button @click.prevent="changeHomePage('allFav')"> All Favorite </button>
      </div>
      <div v-else-if="homePage == 'allFav'">
        <AllFavorite></AllFavorite>
        <button @click.prevent="changeHomePage('allMusic')"> All Music </button>
      </div>
      <Navbar @logout="logout()" @fetchAllSong="fetchAllSong()"></Navbar>
      <Main :homePage="homePage"></Main>
  </div>
</template>

<script>
import Navbar from './Navbar'
import Main from './Main'

import AllFavorite from './AllFavorite'
import AllMusic from './AllMusic'
import server from "../apis/server";
const { serverURL, Swal, axios } = server;


export default {
    data : function(){
        return {
            homePage : "allMusic",
            allMusic : []
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
        },
        fetchAllSong() {
            const token = localStorage.getItem("token");
            axios({
                method: "GET",
                url: `${serverURL}/music`,
                headers: {
                token
                }
            })
            .then(response => {
                this.allMusic = response.data;
                console.log(this.allMusic);
            })
            .catch(err => {
                console.log("ERR");
                console.log( JSON.stringify( err , null , 2 ) );
            });
        }
    },
    created : function(){
        this.fetchAllSong();
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