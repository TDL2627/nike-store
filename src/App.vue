<template>

  <router-view/>
</template>

<script>
import Navbar from "./components/Navbar.vue";
export default {
  components:{Navbar},
  data(){
    return{
     
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color:black;
  height:100vh;
  color: #2c3e50;
}
*{
  font-family: 'Oswald', sans-serif;
}

</style>
