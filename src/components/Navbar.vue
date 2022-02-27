<template>
   <div id="nav">
    <router-link to="/">Home</router-link> |
<div v-if="isLoggedIn">
   <router-link  to="/login">Login</router-link> |
    <router-link to="/register">Register</router-link>

</div>

    

    <div v-else>
  <router-link  to="/products">Products</router-link> |
   <router-link to="/cart">Cart</router-link>  |
    </div>
  
    

<!-- 
  <router-link to="/contact">Contact</router-link> -->

  </div>
</template>

<script>
export default {
props:['isLoggedIn']
}
</script>

<style scoped>

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
    width: 400px !important;
}

#nav a.router-link-exact-active {
  color: red;
}
</style>