<template>
  <h1>Products</h1>

<div class="container">
<div class="row">

<div v-for="product of products" :key="product.name" class="card col-lg-4">
<img :src="product.img" alt="pik" class="pic">
<h3>{{product.name}}</h3>
<p>{{product.price}}</p>
<p>{{product.category}}</p>
<button>delete</button>
<button>edit</button>
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
          alert("User not loggen  in");
        });
    } else {
      alert("User not logged in");
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
  width: max-content;
  object-fit:cover ;
}
</style>