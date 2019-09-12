<template>
    <div>
        REGISTER
        <form @submit.prevent="register()">
            <input type="text" v-model='registerEmail'>
            <input type="text" v-model='registerPassword'>
            <input type="submit" value="Register">
        </form>
        <button @click.prevent="loginPage()">Login</button>
    </div>
</template>

<script>
import server from '../apis/server';
const { axios , serverURL, Swal } = server

export default {
    data : function () {
        return {
            registerEmail : "",
            registerPassword : ""
        }
    },
    methods : {
        register() {
            axios({
                method: "POST",
                url : `${serverURL}/register`,
                data : {
                    email : this.registerEmail,
                    password : this.registerPassword
                }
            })
            .then( response => {
                this.$emit('register' , 'Register' , 'Your Account has been registered')
            })
            .catch( err => {
                console.log( err );
                this.$emit('error' , 'Error' , 'Register Failed')
            })
        },
        loginPage() {
            this.$emit('loginPage', 'login')
        }
     }
}
</script>

<style>

</style>