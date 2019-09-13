<template>
  <div>
    <button @click.prevent="fav( id )" class="btn music-main-btn">Unfavorite</button>
  </div>
</template>

<script>
import server from "../apis/server";
const { serverURL, axios, Swal } = server;
export default {
  data: function() {
    return {};
  },
  props: ["id"],
  methods: {
    fav: function(id) {
      const token = localStorage.getItem("token");
      axios({
        method: "PATCH",
        url: `${serverURL}/music/unfavorite/${id}`,
        headers: {
          token
        }
      })
        .then(response => {
          Swal.fire({
            type: "success",
            text: "Success remove favorite"
          });
        })
        .catch(err => {
          Swal.fire({
            type: "error",
            text: "already fav"
          });
          console.log("eRROR FAVORITE BUTTON");
          console.log(JSON.stringify(err.response, null, 2));
        });
    }
  }
};
</script>

<style scoped>
.music-main-btn {
  border: 3px solid gray;
  font-weight: bolder;
  color: grey;
  transition: 0.7s all;
}
.music-main-btn:hover {
  border: 3px solid gray;
  font-weight: bolder;
  background-color: grey;
  color: whitesmoke;
  transition: 0.7s all;
}
</style>