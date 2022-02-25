<template>
   <div id="nav">
    <router-link to="/">Home</router-link> |

  <router-link  to="/products">Products</router-link> |
   <router-link to="/cart">Cart</router-link>  |
    

    
   <router-link  to="/login">Login</router-link> |
    <router-link to="/register">Register</router-link>
    

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
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>