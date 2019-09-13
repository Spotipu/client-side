<template>
     <div>
        <b-container>
            <b-card class="my-5"
            header="Login"
            >
                <b-form @submit.prevent="register()">
                    <b-form-group
                id="input-group-1"
                label="Email address:"
                label-for="input-1"
                description="We'll never share your email with anyone else."
                >
                    <b-form-input
                        id="input-1"
                        v-model="registerEmail"
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
                        v-model="registerPassword"
                        type="password"
                        required
                        placeholder="Enter password"
                        ></b-form-input>
                    </b-form-group>
                    <b-button type="submit" variant="primary">Register</b-button>
                    <b-button id="toLogin" @click.prevent="loginPage()" variant="warning">Login Here</b-button>
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
    #toLogin {
        float: right
    }
</style>