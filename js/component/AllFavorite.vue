<template>
    <b-container>
    <b-row>
      <h3>All Favoites</h3>
    </b-row>
    <b-row>
      <b-col class="my-3" cols="12" v-for="fav in myFavorites" :key="fav._id">
          <b class="card">
            <Audio :title="fav.title" :artist="fav.artist" :file="fav.url"  @fetchAllSong="fetchAllSong()"></Audio>
            <div>
                <UnFavoriteButton :id="fav._id" @fetchAllSong="fetchAllSong ()"></UnFavoriteButton>
            </div>            
          </b>
      </b-col>
    </b-row>
  </b-container>

    <!-- <div>
        <h1>All Favorites</h1>
        <div v-if="myFavorites.length == 0 ">
            <h2>No Fav</h2>
        </div>
        <div v-else>
            <div v-for="fav in myFavorites" :key="fav._id">
                <Audio :file="fav.url"></Audio>
                <div>
                    <UnFavoriteButton :id="fav._id" @unFav="fetchAllFavorites()"></UnFavoriteButton>
                </div>
            </div>
        </div>
    </div> -->
</template>

<script>
import server from '../apis/server';
import Audio from './Audio'
import UnFavoriteButton from './UnFavoriteButton'

const { axios, serverURL , Swal } = server
export default {
    data : function () {
        return  {
        }
    },
    props : ["myFavorites"],
    methods : {
        // fetchAllFavorites () {
        //     const token = localStorage.getItem('token')
        //     axios({
        //         method : "GET",
        //         url : `${serverURL}/music/favorite`,
        //         headers : {
        //             token
        //         }
        //     })
        //     .then( response => {
        //         this.myFavorites = response.data;
        //     })
        //     .catch( err => {
        //         console.log("ERR")
        //         console.log( err );
        //     }) 
        // },
        fetchFav() {
            this.$emit('fetchAllFavorites')
        },
        fetchAllSong(){
            this.$emit('fetchAllSong')
        }
    },
    created : function() {
        this.fetchFav()
    },
    components : {
        Audio,
        UnFavoriteButton
    }
}

</script>








<style scoped>
 

</style>