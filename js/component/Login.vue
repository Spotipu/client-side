<template>
  <div>
      LOGIN
        <span v-if="(errorMessage.length != 0)">{{ errorMessage }}</span>
        <form @submit.prevent="login()">
            <input type="text" v-model='email'>
            <input type="text" v-model='password'>
            <input type="submit" value="Login">
        </form>
        <button @click.prevent="registerPage()"> Register Here </button>
  </div>
</template>

<script>
import server from '../apis/server';
const { axios , serverURL, Swal } = server
export default {
    data : function () {
        return {
            email : "", 
            password : "",
            errorMessage : ""
        }
    },
    methods : {
        login: function () {
            axios({
                method: "POST",
                url : `${serverURL}/login`,
                data : {
                    email : this.email,
                    password: this.password
                }
            })
            .then ( response => {
                const { token } = response.data;
                // Emit param1 ( yang trigger bapak , bwt params)
                this.$emit('login', {
                    page: 'home',
                    status: 'success',
                    title : "Login",
                    message: 'Success!',
                    email : this.email
                });

                localStorage.setItem('token' , token ) ;

                this.email = '';
                this.password = '';
            })
            .catch ( err => {
                this.errorMessage = 'Invalid Email/Password';
            })
        },
        registerPage : function (){
            this.$emit('registerPage' , 'register')
        }
    }
}
</script>

<style>

</style>