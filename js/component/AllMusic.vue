<template>
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