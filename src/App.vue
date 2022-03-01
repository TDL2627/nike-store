<template>

  <router-view/>
</template>

<script>
// Componenets of different sections
import Navbar from "./components/Navbar.vue";
import TheLoader from "./components/TheLoader.vue";


export default {
  components:{Navbar,TheLoader},
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
  overflow-y: scroll;
}
*{
  font-family: 'Oswald', sans-serif;
}

</style>
