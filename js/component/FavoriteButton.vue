<template>
    <div>
        <button @click.prevent="fav( id )">Favorite</button>
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
        fav : function ( id ) {
            const token = localStorage.getItem('token')
            axios({
                method :"PATCH",
                url : `${serverURL}/music/favorite/${id}`,
                headers : {
                    token
                }
            })
            .then( response => {
                Swal.fire({
                    type: 'success',
                    text: "FAV"
                })
            })
            .catch( err => {
                
                Swal.fire({
                    type: 'error',
                    text: "already fav"
                })
                console.log("eRROR FAVORITE BUTTON")
                console.log( JSON.stringify( err.response , null , 2) );
            })
            
        }
    }
}
</script>

<style>

</style>