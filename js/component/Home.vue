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

          <div id="plus-song">
            <b-form @submit.prevent="addSong()">
                    <b-form-group
                    label="Music File"
                    label-for="music-file"
                    >   
                        <b-form-file
                        v-on:change="handlefileupload($event)"
                        lang="es"
                        accept=".mp3"
                        class="mt-3" 
                        plain>
                        </b-form-file>
                        <div class="mt-3">Selected file: {{ file2 ? file2.name : '' }}</div>
                    
                    </b-form-group>
                   
                    <b-form-group id="input-group-2" label="Artist" label-for="input-2">
                        <b-form-input
                        id="input-2"
                        v-model="artist"
                        required
                        placeholder="Artist Name"
                        ></b-form-input>
                    </b-form-group>

                     <b-form-group id="input-group-3" label="Title" label-for="input-3">
                        <b-form-input
                        id="input-3"
                        v-model="title"
                        required
                        placeholder="Title"
                        ></b-form-input>
                    </b-form-group>

                    <b-button type="submit" variant="warning">Add Song</b-button>
                </b-form>


            <!-- <form @submit.prevent="addSong()">
                Your Song file Here:
                <input
                type="file"
                v-on:change="handlefileupload($event)"
                lang="es"
                accept=".mp3"
                />
                Artist
                <input type="text" v-model="artist" />
                Title
                <input type="text" v-model="title" />
                <input type="submit" value="add song" />
            </form> -->
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
            allMusic : [],
            file: "",
            artist: "",
            title: ""
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
        },
        handlefileupload(event) {
            let file = event.target.files || event.dataTransfer.files;
            this.file = file[0];
            },
            addSong() {
      const token = localStorage.getItem("token");
      let formData = new FormData();
      formData.set("file", this.file);
      formData.set("title", this.title);
      formData.set("artist", this.artist);
      axios({
        method: "POST",
        url: `${serverURL}/music/upload`,
        data: formData,
        headers: {
          token
        }
      })
        .then(({ data }) => {
          Swal.fire({
            type: "success",
            text: "Song Added!"
          });
          this.$emit("fetchAllSong");
        })
        .catch(err => {
          console.log(err);
          Swal.fire({
            type: "error",
            text: "error Addsong!"
          });
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
    #plus-song {
        padding: 20px;
    }

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
        padding: 10px 20px;
        font-size: 14px;
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