<template>


 <div class="cart">
<the-loader></the-loader>
    <nav class="navbar navbar-expand-lg navbar-light bg-dark fixed-top">
  <div class="container-fluid">
   <h1>CART</h1>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <div class="navg ">
         <router-link class="nav-link" to="/products">PRODUCTS</router-link>
            <router-link class="nav-link" to="/profiles">PROFILE</router-link>
            <router-link class="nav-link" to="/">LOG OUT</router-link>
    </div>

    </div>
  </div>
</nav>

<h1>in development ...</h1>
<h1>coming soon</h1>
<h3>server cart functions not linked to front-end yet...</h3>
 </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.cart{
  padding-top:15%;
}
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
  display: inline-flex;
  right: 5px;
}
@media only screen and (max-width: 500px) {
 .navg{
  position: relative;
  display: initial;
}
}

</style>