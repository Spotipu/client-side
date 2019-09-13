<template>
    <div>
        <button @click.prevent="unFav( id )">UnFavorite</button>
    </div>
</template>

<script>
import server from '../apis/server';
const { serverURL , axios , Swal } = server
export default {
    data : function() {
        return {

        }
    },
    props : ['id'],
    methods : {
        unFav : function ( id ) {
            const token = localStorage.getItem('token')
            axios({
                method :"PATCH",
                url : `${serverURL}/music/unfavorite/${id}`,
                headers : {
                    token
                }
            })
            .then( response => {
                Swal.fire("Success" , "Unfavorite!")
                this.$emit('fetchAllSong');
            })
            .catch( err => {
                console.log("eRROR UNFAVORITE BUTTON")
                console.log( err );
            })
            
        }
    }
}
</script>

<style>

</style>