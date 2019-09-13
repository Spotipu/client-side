<template>
<<<<<<< HEAD
  <div class="d-flex flex-column justify-content-center">
    <h1 class="text-center mt-5">All Music</h1>
    <div class="row d-flex justify-content-center align-items-start mt-5">
      <div
        v-for="music in allMusic"
        :key="music._id"
        class="shadow-lg m-2 col-12 col-sm-12 col-md-12 col-lg-6 col-xl-6"
      >
        <Audio :file="music.url" :id="music._id"></Audio>
      </div>
    </div>
=======
  <div>
      <b-container>
          <b-row>
              <h3>All Music</h3>
          </b-row>
          <b-row>
              <b-col cols="3">
                <div v-for="music in allMusic" :key="music._id">
                    <b-card
                    header="Nama Lagu">
                        <Audio :file="music.url"></Audio>                        
                    </b-card>
                </div>
              </b-col>
          </b-row>
      </b-container>
>>>>>>> add layout
  </div>
</template>

<script>
import server from "../apis/server";
import Audio from "../component/Audio";
import FavoriteButton from "./FavoriteButton";

const { axios, serverURL, Swal } = server;

export default {
  data: function() {
    return {
      allMusic: []
    };
  },
  methods: {
    fetchAllMusic() {
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
    fetchFavMusic() {
      this.$emit("fetchFavMusic");
    }
  },
  created: function() {
    this.fetchAllMusic();
  },
  components: {
    Audio,
    FavoriteButton
  }
};
</script>

<style>
</style>