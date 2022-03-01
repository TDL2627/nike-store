<template>


<div><Cart/></div>

  

   
</template>

<script>
import Cart from "@/components/Cart-c.vue";
export default {
  components:{Cart},

}
</script>

<style scoped>

h1,h5,h3{
  color:red;
}
.nav-link{
  color:white !important;
}
.nav-link:hover{
  color:red !important;
}
.nav-link:focus{
  color:red !important;
}
ul{
  list-style: none;
}
.droppie{
  border: none;
  background: none;
  padding-left: 50px;
}
.droppie:hover{
color: red;
  background: none;
  padding-left: 50px;
}
.navg{
  position: fixed;
  
  right: 5px;
}
</style>