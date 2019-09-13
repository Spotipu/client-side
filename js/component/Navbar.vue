<template>
  <div id="navbar-spo">
    <img class="my-4" width="60%" src="../static/logo.png" alt />

    <NavbarItem :name="'All Music'"></NavbarItem>
    <NavbarItem :name="'My Music'"></NavbarItem>
    <NavbarItem :name="'Favorites'" @changeHomePage="changeHomepage('allFav')"></NavbarItem>
    <NavbarItem :name="'Logout'" @logout="logout()"></NavbarItem>
    <div>
      <form @submit.prevent="addSong()">
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
      </form>
    </div>
  </div>
</template>

<script>
import NavbarItem from "./NavbarItem";
import server from "../apis/server";
const { serverURL, Swal, axios } = server;

export default {
  data: function() {
    return {
      file: "",
      artist: "",
      title: ""
    };
  },
  components: {
    NavbarItem
  },
  methods: {
    handlefileupload(event) {
      let file = event.target.files || event.dataTransfer.files;
      this.file = file[0];
    },
    logout() {
      console.log("navbar");
      this.$emit("logout");
    },

    changeHomePage(page) {
      this.$emit("changeHomePage");
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
  }
};
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
</style>