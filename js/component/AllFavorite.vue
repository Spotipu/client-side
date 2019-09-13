<template>
    <div>
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
    </div>
</template>

<script>
import server from '../apis/server';
import Audio from './Audio'
import UnFavoriteButton from './UnFavoriteButton'

const { axios, serverURL , Swal } = server
export default {
    data : function () {
        return  {
            myFavorites : []
        }
    },
    methods : {
        fetchAllFavorites () {
            const token = localStorage.getItem('token')
            axios({
                method : "GET",
                url : `${serverURL}/music/favorite`,
                headers : {
                    token
                }
            })
            .then( response => {
                this.myFavorites = response.data;
            })
            .catch( err => {
                console.log("ERR")
                console.log( err );
            }) 
        }
    },
    created : function (){
        this.fetchAllFavorites()
    },
    components : {
        Audio,
        UnFavoriteButton
    }
}

</script>








<style scoped>
 

</style>