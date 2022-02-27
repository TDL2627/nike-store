<template>
  <div class="home">
    <h1>THIS IS THE NIKE STORE</h1>
<div class="linky">
 <router-link  to="/login">Login</router-link> |
    <router-link to="/register">Register</router-link>
</div>
     
  </div>
</template>

<script>

export default {
 
}
</script>

<style scoped>
a{
  border: 2px solid black;
  border-radius: 25px;
  padding: 15px;

}
.linky{
    position: fixed;
  bottom: 5%;
  left: 40%;
}
</style>