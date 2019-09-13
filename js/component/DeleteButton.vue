<template>
    <div>
        <button @click.prevent="deleteMusic( id )">Delete</button>
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
        deleteMusic : function ( id ) {
            const token = localStorage.getItem('token')
            axios({
                method :"DELETE",
                url : `${serverURL}/music/${id}`,
                headers : {
                    token
                }
            })
            .then( response => {
                Swal.fire({
                    type: 'success',
                    text: "Deleted!"
                })
            })
            .catch( err => {
                
                Swal.fire({
                    type: 'error',
                    text: "Delete Error"
                })
                console.log("eRROR DELETE BUTTON")
                console.log( JSON.stringify( err.response , null , 2) );
            })
            
        }
    }
}
</script>

<style>

</style>