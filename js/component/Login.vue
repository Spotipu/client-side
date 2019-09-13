<template>
    <div>
      <b-container>          
        <span v-if="(errorMessage.length != 0)">{{ errorMessage }}</span>
        <b-card class="my-5"
        header="Login"
        >

            <b-form @submit.prevent="login()">
                <b-form-group
                id="input-group-1"
                label="Email address:"
                label-for="input-1"
                description="We'll never share your email with anyone else."
                >
                    <b-form-input
                    id="input-1"
                    v-model="email"
                    type="email"
                    required
                    placeholder="Enter email"
                    ></b-form-input>
                </b-form-group>

                <b-form-group
                id="input-group-2"
                label="Password:"
                label-for="input-2"
                >
                    <b-form-input
                    id="input-2"
                    v-model="password"
                    type="password"
                    required
                    placeholder="Enter password"
                    ></b-form-input>
                </b-form-group>
                <b-button type="submit" variant="primary">Login</b-button>
                <b-button id="toRegister" @click.prevent="registerPage()" variant="warning">Register Here</b-button>
            </b-form>
            <hr>
        </b-card>
      </b-container>      
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
    #toRegister {
        float : right
    }
</style>