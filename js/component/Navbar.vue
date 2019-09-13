<template>
  <div id="navbar-spo">
      <img class="my-4" width="60%" src="../static/logo.png" alt="">
      
      <NavbarItem :name="'All Music'" ></NavbarItem>
      <NavbarItem :name="'My Music'" ></NavbarItem>
      <NavbarItem :name="'Favorites'" @changeHomePage="changeHomepage('allFav')"></NavbarItem>
      <NavbarItem :name="'Logout'" @logout="logout()" ></NavbarItem>

  </div>
</template>

<script>
import NavbarItem from './NavbarItem'

export default {
    components : {
        NavbarItem
    },
    methods : {
         logout() {
            console.log('navbar')
            this.$emit('logout')
        },

        changeHomePage( page ) {
            this.$emit('changeHomePage')
        }
    }
}

</script>

<style>
    #navbar-spo {
        position: fixed;
        z-index: 999;
        left: 0;
        top: 0;
        height: 100vh;
        width: 300px;
        display: flex;
        flex-direction: column;
        background-color: #1c1c1c;
        align-items: center;
        z-index: 999;
        box-shadow: 0 1px 6px rgba(0, 0, 0, 0.1);
    }
</style>