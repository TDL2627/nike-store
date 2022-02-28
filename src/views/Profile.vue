<template>
  <div class="profile">
      
    <nav class="navbar navbar-expand-lg navbar-light bg-dark fixed-top">
  <div class="container-fluid">
   <h1 style="margin-right:50px;">PROFILE</h1>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <div class="navg d-flex">
         <router-link class="nav-link" to="/products">PRODUCTS</router-link>
            <router-link class="nav-link" to="/cart">CART</router-link>
            <router-link class="nav-link" to="/">LOG OUT</router-link>
    </div>

    </div>
  </div>
</nav>
  </div>
</template>

<script>
export default {

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