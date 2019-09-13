<template>
  <b-container>
    <b-row>
      <h3>All Music</h3>
    </b-row>
    <b-row>
      <b-col class="my-3" cols="12" v-for="music in allMusic"
        :key="music._id">
          <b class="card">
            <Audio :file="music.url" :id="music._id"></Audio>
          </b>
      </b-col>
    </b-row>
  </b-container>

  <!-- <div class="d-flex flex-column justify-content-center">
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
  </div> -->
</template>

<script>
import server from "../apis/server";
import Audio from "../component/Audio";
import FavoriteButton from "./FavoriteButton";

const { axios, serverURL, Swal } = server;

export default {
  data: function() {
    return {
    };
  },
  props: ['allMusic'],
  methods: {
    
    fetchFavMusic() {
      this.$emit("fetchFavMusic");
    }
  },
 
  components: {
    Audio,
    FavoriteButton
  }
};
</script>

<style>
</style>