<template>
  <div>
      <button @click.prevent='logout()'>Logout</button>
  </div>
</template>

<script>
export default {
    data : function(){
        return {
            
        }
    },
    methods : {
        logout() {
            localStorage.removeItem('token');
            this.$emit('logout');
        }
    }
}
</script>

<style>
    
</style>