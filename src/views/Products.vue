<template>
<div class="products">
 

  <nav class="navbar navbar-expand-lg navbar-light bg-dark fixed-top">
  <div class="container-fluid">
   <h1>Products</h1>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
            <!-- Button trigger modal for add product -->
<a class="nav-link" style="cursor:pointer;" data-bs-toggle="modal" data-bs-target="#exampleModal">
  Add a product
</a>
        </li>
        
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Sort by
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
            <li><button>Price</button></li>
              <li><hr class="dropdown-divider"></li>
            <li><button>Name</button></li>
          
          </ul>
        </li>
         <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown1" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Catergory
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdown1">
            <li><button>Shoes</button></li>
              <li><hr class="dropdown-divider"></li>
            <li><button>Accessories</button></li>
            <li><hr class="dropdown-divider"></li>
            <li><button>Clothing</button></li>
          </ul>
        </li>
        <li>
          <form class="d-flex">
             <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
                     <button class="btn btn-outline-danger" type="submit">Search</button>
          </form>
        </li>
      </ul>
         <router-link class="nav-link" to="/cart">TILL</router-link>
            <router-link class="nav-link" to="/profiles">PROFILES</router-link>
    </div>
  </div>
</nav>


<!-- Modal for add  product -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Add Nike</h5>
        
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
       <form action="">
    <ul>
      <li>NAME</li>
      <li> <input type="text"></li>
      <li>PRICE</li>
<li> <input type="number"></li>
<li>IMAGE URL</li>
<li> <input type="text"></li>
           <li>Shoes<input style="margin:10px;" type="radio">Accessories<input style="margin:10px;" type="radio">Clothing<input style="margin:10px;" type="radio"></li>
         </ul>
          <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
       </form>
      </div>
     
    </div>
  </div>
</div>

<!-- Modal for edit  product -->
<div class="modal fade" id="exampleModal1" tabindex="-1" aria-labelledby="exampleModalLabel1" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">EDIT NIKE</h5>
        
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
       <form action="">
    <ul>
      <li>NAME</li>
      <li> <input type="text"></li>
      <li>PRICE</li>
<li> <input type="number"></li>
<li>IMAGE URL</li>
<li> <input type="text"></li>
           <li>Shoes<input style="margin:10px;" type="radio">Accessories<input style="margin:10px;" type="radio">Clothing<input style="margin:10px;" type="radio"></li>
         </ul>
          <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
       </form>
      </div>
     
    </div>
  </div>
</div>

  
<div class="container">
<div class="row">

<div v-for="product of products" :key="product.name" class="card col-lg-3">
<img :src="product.img" alt="pik" class="pic">
<h3>{{product.name}}</h3>
<p>R{{product.price}}</p>
<p>{{product.category}}</p>
<button>DELETE</button>
<button class="button" style="cursor:pointer;" data-bs-toggle="modal" data-bs-target="#exampleModal1">
  EDIT 
</button>
</div>

</div>
</div>
      




</div>


</template>

<script>
export default {

  data() {
    return {
      products: null,
    };
  },
  // fetching product
  mounted() {
    if (localStorage.getItem("jwt")) {
      fetch("https://nike-store-api.herokuapp.com/products", {
        method: "GET",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.products = json;
          this.products.forEach(async (product) => {
            await fetch(
              "https://nike-store-api.herokuapp.com/products/" + product.author,
              {
                method: "GET",
                headers: {
                  "Content-type": "application/json; charset=UTF-8",
                  Authorization: `Bearer ${localStorage.getItem("jwt")}`,
                },
              }
            )
              .then((response) => response.json())
              .then((json) => {
                product.author = json.name;
              });
          });
        })
        .catch((err) => {
          alert("Not logged in");
          this.$router.push({ name: "Login" })
        });
    } else {
      alert("Login failed");
      this.$router.push({ name: "Login" });
    }
    
  },
};
</script>

<style scoped>
.products{
  padding-top: 7%;
   padding-bottom: 7%;
   padding-left: 7%;
}
.card{
  border: 2px solid black;
  margin: 20px;
}
.pic{
  height: 250px;
  width: 100%;
  object-fit:cover ;
}
h1,h5{
  color:red;
}
.nav-link{
  color:white !important;
}
ul{
  list-style: none;
}

</style>