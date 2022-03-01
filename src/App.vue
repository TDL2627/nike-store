<template>

  <router-view/>
  <Footer/>
</template>

<script>
// Componenets of different sections
import Navbar from "./components/Navbar.vue";
import TheLoader from "./components/TheLoader.vue";
import Footer from "./components/Footer.vue";

export default {
  components:{Navbar,TheLoader,Footer},
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
width: 100%;
margin: 0;
padding: 0;
  color: #2c3e50;
  overflow-y: none;
}
/* width */
::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  background: whitesmoke; 
}
 
/* Handle */
::-webkit-scrollbar-thumb {
  background: red; 
  border-radius: 25px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: rgb(199, 70, 70); 
}
*{
  font-family: 'Oswald', sans-serif;
}

</style>
