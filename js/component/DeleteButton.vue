<template>
  <div>
    <button @click.prevent="deleteMusic( id )" class="btn music-main-btn">Delete</button>
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
    deleteMusic: function(id) {
      console.log(this.id)
      console.log(`aaaaaaaaaaaa`);
      const token = localStorage.getItem("token");
      axios({
        method: "DELETE",
        url: `${serverURL}/music/${id}`,
        headers: {
          token
        }
      })
        .then(response => {
          Swal.fire({
            type: "success",
            text: "Deleted!"
          });
          this.$emit("fetchAllSong");

        })
        .catch(err => {
          Swal.fire({
            type: "error",
            text: "Delete Error"
          });
          console.log("eRROR DELETE BUTTON");
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