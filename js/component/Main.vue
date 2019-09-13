<template>
  <div>
    <div id="main-spo">
       <b-container>
         <b-row>
           <p>
           {{ homePage }}

           </p>
         </b-row>
       </b-container>
    </div>
  </div>
</template>

<script>
export default {
  props : ['homePage']
}
</script>

<style>
    #main-spo {
        height: 100vh;
        position: relative;
        display: flex;
        width: calc(100% - 300px);
        align-items: center;
        margin: 0px 0px 0px 300px;
        padding: 60px 0px;
        background: #1e293a;
    }
</style>