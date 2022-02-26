<template>
<div class="products">
  <h1>Products</h1>
  <!-- Button trigger modal -->
<button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
  Add a product
</button>

<!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Add Nike</h5>
        
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        ...
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
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
<button>delete</button>
<button>edit</button>
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
          alert("Log in failed");
        });
    } else {
      alert("Not logged in");
      this.$router.push({ name: "Login" });
    }
    
  },
};
</script>

<style scoped>
.card{
  border: 2px solid black;
  margin: 20px;
}
.pic{
  height: 250px;
  width: 100%;
  object-fit:cover ;
}
</style>