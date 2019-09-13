<template>
  <div @click.prevent="navFunction()" class="navbar-item">
      {{ name }}
  </div>
</template>

<script>
export default {
    data : function() {
        return {

        }
    },
    props: ['name'],
    methods : {
        navFunction(){
            if(this.name === "All Music"){
                this.$emit('changeHomePage', 'allMusic')
                console.log("a")
            } else if ( this.name === "My Music" ) {
                this.$emit('changeHomePage', 'myMusic')

                console.log("b")
            } else if ( this.name === "Favorites" ) {
                this.$emit('changeHomePage', 'myFav')

                console.log("c")
            } else if ( this.name === "Logout" ) {
                console.log("logout clicked")
                this.logout()
            }
        },

        logout() {
            console.log('item')
            this.$emit('logout')
        }
    }
}
</script>

<style>
    .navbar-item {
        width: 100%;
        margin: 0px;
        padding: 20px 20px;
        font-size: 18px;
        font-weight: 700;
        text-align: left;
        color: white;
        background: #1c1c1c;
    }

    div.navbar-item:hover {
        cursor: hand;
        cursor: pointer;
        color: #1c1c1c;
        background: #5bba55;
    }
</style>