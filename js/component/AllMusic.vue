<template>
  <div class="d-flex flex-column justify-content-center">
    <h1 class="text-center mt-5">All Music</h1>
    <div class="row d-flex justify-content-center align-items-start mt-5">
      <div
        v-for="music in allMusic"
        :key="music._id"
        class="shadow-lg m-2 col-12 col-sm-12 col-md-12 col-lg-6 col-xl-6"
      >
        <Audio :file="music.url" :id="music._id"  @fetchAllSong="fetchAllSong()"></Audio>
      </div>
    </div>
  </div>
</template>

<script>
import server from "../apis/server";
import Audio from "../component/Audio";
import FavoriteButton from "./FavoriteButton";

const { axios, serverURL, Swal } = server;

export default {
  data: function() {
    return {};
  },
  props: ["allMusic"],
  methods: {
    fetchAllSong() {
      this.$emit("fetchAllSong");
    },
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