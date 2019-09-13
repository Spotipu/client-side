<template>
    <b-container>
    <b-row>
      <h3>My Music</h3>
    </b-row>
    <b-row>
      <b-col class="my-3" cols="12" v-for="music in myMusic" :key="music._id">
          <b class="card">
            <Audio :file="music.url"></Audio>
          </b>
      </b-col>
    </b-row>
  </b-container>

    <!-- <div>
        <h1>My Music</h1>
        <Audio v-for="music in myMusic" :key="music._id" :file="music.url"></Audio>
    </div> -->
</template>

<script>
import Audio from './Audio'
import server from '../apis/server'

const { serverURL , axios } = server

export default {
    data : function () {
        return {
            myMusic : []
        }
    },
    methods : {
        fetchMyMusic : function () {
            const token = localStorage.getItem('token');
            axios({
                method : "GET",
                url : `${serverURL}/music/mymusic`,
                headers :{
                    token
                }
            })
            .then( response => {
                this.myMusic = response.data
            })
            .catch( err => {
                console.log( 'err');
            })
        }
    },
    created: function() {
        this.fetchMyMusic();
    },
    components : {
        Audio
    }
}
</script>

<style>

</style>