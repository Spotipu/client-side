<template>
    <div>
        <div v-if="currentPage == 'login'">
            <!-- yang trigger bapak = fungsi bapak  -->
            <Login @login="loginForm" @registerPage="changePage"></Login>
        </div>
        <div v-else-if="currentPage == 'register'">
            <Register @register="register" @error="showError" @loginPage='changePage'></Register>
        </div>
        <div v-else-if="currentPage == 'home'">
            


            <Home @logout="logout" ></Home>
        </div>
    </div>
</template>

<script>
// Component
import Login from './component/Login';
import Register from './component/Register';
import Home from './component/Home';
// Helper
import server from './apis/server';
const { axios , serverURL, Swal } = server;

export default {
    data() {
        return {
            currentPage : 'login',
            username : ""
        };
    },
    methods: {
        showSuccess ( title, message ) {
            Swal.fire({
                type: 'success',
                title,
                text: message
            })
        },
        showError ( title,  message ) {
            Swal.fire({
                type: 'error',
                title,
                text : message
            })
        },
        loginForm({ page , status, title , message }) {
            
            if ( status == 'success'){
                this.changePage('home')
                this.showSuccess ( title, message) ;
            } else if ( status == 'error') {
                this.changePage('login')
                this.showError( title ,message );
            }
        },
        register ( title , message ) {
            this.changePage('login')
            this.showSuccess(status, message)
        },
        changePage ( page ) {
            this.currentPage = page;
        },
        logout() {
            this.changePage('login');
        }
    },
    components: {
        Login,
        Register,
        Home
    },
    created : function() {
        const token = localStorage.getItem('token')
        if ( token ) {
            this.changePage('home')
        } else {
            this.changePage('login')
        }
    }
}
</script>

<style scoped>

</style>