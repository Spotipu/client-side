<template>
  <div>
      <h1>All Music</h1>
      <div v-for="music in allMusic" :key="music._id">
        <Audio :file="music.url"></Audio>
      </div>
  </div>
</template>

<script>
import server from '../apis/server';
import Audio from '../component/Audio'
const { axios, serverURL , Swal } = server

export default {
    data : function () {
        return  {
            allMusic : []
        }
    },
    methods : {
        fetchAllMusic () {
            const token = localStorage.getItem('token')
            axios({
                method : "GET",
                url : `${serverURL}/music`,
                headers : {
                    token
                }
            })
            .then( response => {
                this.allMusic = response.data;
                console.log( this.allMusic )
            })
            .catch( err => {
                console.log("ERR")
                console.log( err );
            }) 
        }
    },
    created : function (){
        this.fetchAllMusic()
    },
    components : {
        Audio
    }
}
</script>

<style>

</style>