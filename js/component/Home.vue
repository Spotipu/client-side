<template>
  <div>
      <div id="navbar-spo">
          <img class="my-4" width="60%" src="../static/logo.png" alt />

          <div @click.prevent="changeHomePage('allMusic')" class="navbar-item">
              All Music
          </div>
          <div @click.prevent="changeHomePage('myMusic')" class="navbar-item">
              My Music
          </div>
          <div @click.prevent="changeHomePage('allFav')" class="navbar-item">
              Favorites
          </div>
          <div @click.prevent="logout()" class="navbar-item">
              Logout
          </div>
      </div>

      <div id="main-spo">
             <div v-if="homePage == 'allMusic'">
                <AllMusic :allMusic='allMusic'></AllMusic>
            </div>
            <div v-else-if="homePage == 'allFav'">
                <AllFavorite></AllFavorite>
            </div>
            <div v-else-if="homePage == 'myMusic'">
               <MyMusic></MyMusic>
            </div>
      </div>    
  
  </div>
</template>

<script>

import AllFavorite from './AllFavorite'
import AllMusic from './AllMusic'
import MyMusic from './MyMusic'
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
        MyMusic
    }
}
</script>

<style>
    #navbar-spo {
  position: fixed;
  z-index: 999;
  left: 0;
  top: 0;
  height: 100vh;
  width: 300px;
  display: flex;
  flex-direction: column;
  background-color: #1c1c1c;
  align-items: center;
  z-index: 999;
  box-shadow: 0 1px 6px rgba(0, 0, 0, 0.1);
}

.navbar-item {
        width: 100%;
        margin: 0px;
        padding: 20px 20px;
        font-size: 18px;
        font-weight: 700;
        text-align: left;
        color: white;
        background: #1c1c1c;
    }

    div.navbar-item:hover {
        cursor: hand;
        cursor: pointer;
        color: #1c1c1c;
        background: #5bba55;
    }

     #main-spo {
        height: 100vh;
        position: relative;
        display: flex;
        width: calc(100% - 300px);
        margin: 0px 0px 0px 300px;
        padding: 60px;
    }
</style>