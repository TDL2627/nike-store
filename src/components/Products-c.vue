<template>
<div class="products">
 <the-loader></the-loader>

  <nav class="navbar navbar-expand-lg navbar-light bg-dark fixed-top">
  <div class="container-fluid">
   <h1 style="margin-right:50px;">PRODUCTS</h1>
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
            <li><button class="droppie">Price</button></li>
              <li><hr class="dropdown-divider"></li>
            <li><button class="droppie">Name</button></li>
          
          </ul>
        </li>
         <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown1" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Catergory
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdown1">
            <li><button class="droppie">Shoes</button></li>
              <li><hr class="dropdown-divider"></li>
            <li><button class="droppie">Accessories</button></li>
            <li><hr class="dropdown-divider"></li>
            <li><button class="droppie">Clothing</button></li>
          </ul>
        </li>
        <li>
          <!-- search -->
          <form class="d-flex" @submit.prevent="filteredList">
             <input class="form-control me-2"  type="search" v-model="search" placeholder="Search" aria-label="Search">
                     <button class="btn btn-outline-danger"   type="submit">Search</button>
          </form>
        </li>
      </ul>
       <!-- <router-link class="nav-link" to="/add">ADD A PRODUCT</router-link> -->
         <router-link class="nav-link" to="/cart">CART</router-link>
            <router-link class="nav-link" to="/profiles">PROFILE</router-link>
            <router-link class="nav-link" to="/">LOG OUT</router-link>
    </div>
  </div>
</nav>


<!-- Modal for add  product -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Add Nike</h5>
        
        <button type="button" class="btn-close btn-danger" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
       <form @submit.prevent="createProduct">
        <ul>
          <li>NAME</li>
          <li> <input v-model="name" required type="text"></li>
          <li>PRICE</li>
          <li> <input v-model="price" required type="number"></li>
          <li>IMAGE URL</li>
          <li> <input v-model="img" required  type="text"></li>
<label for="genre">CATEGORY:</label>
<select id="genre" v-model="category" name="genre">
  <option value="Shoes">Shoes</option>
  <option value="Accessories">Accessories</option>
  <option value="Clothing">Clothing</option>

</select>        </ul>

       
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
          <button type="submit" class="btn btn-success">Save changes</button>
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
        
        <button type="button" class="btn-close btn-danger" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
       <form action="">
    <ul>
      <li>NAME</li>
      <li> <input v-model="name" required type="text"></li>
      <li>PRICE</li>
<li> <input v-model="price" required type="number"></li>
<li>IMAGE URL</li>
<li> <input v-model="img" required  type="text"></li>
           <li>Shoes<input v-model="category"  style="margin:10px;" type="radio">Accessories<input v-model="category" style="margin:10px;" type="radio">Clothing<input v-model="category" style="margin:10px;" type="radio"></li>
         </ul>
          <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="submit" class="btn btn-success">Save changes</button>
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
<button type="button" class="btn btn-danger" style="margin:10px;">DELETE</button>
<button type="button" class="btn btn-secondary" style="margin:10px;" data-bs-toggle="modal" data-bs-target="#exampleModal1">
  EDIT 
</button>
</div>

</div>
</div>



</div>

</template>

<script>
import TheLoader from "@/components/TheLoader.vue";
export default {
components:{
  TheLoader
},
  data() {
    return {
      products: null,
      name:"",
      category:"",
      price:"",
      img:"",
       search: "",

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
   methods: {
    createProduct() {
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        return this.$router.push({ name: "Login" });
      }
      fetch("https://nike-store-api.herokuapp.com/products", {
        method: "POST",
        body: JSON.stringify({
          name: this.name,
          category: this.category,
          price: this.price,
          img: this.img,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          alert("Product Created");
          this.$router.push({ name: "Products" });
        })
        .catch((err) => {
          alert(err);
        });
    },
  },
    // search
      computed: {
    filteredList() {
      return this.products.filter(product => {
        return product.name.toLowerCase().includes(this.search.toLowerCase())
       .then(
            alert("search not working")
       )
      })
      
    }
      }
};
</script>

<style scoped>
.products{
  padding-top: 7%;
   padding-bottom: 7%;
   padding-left: 8%;
   height: 100vh;
   overflow-y: scroll;
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

@media only screen and (max-width: 500px) {
.products{
    padding-top: 15%;
    padding-bottom: 15%;
}
.card{
    width: 80%;
}

}
</style>