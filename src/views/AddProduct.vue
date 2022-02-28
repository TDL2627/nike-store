<template>
  <div class="adding">

      <form @submit.prevent="createProduct">
        <ul>
          <li>NAME</li>
          <li> <input v-model="name" required type="text"></li>
          <li>PRICE</li>
          <li> <input v-model="price" required type="number"></li>
          <li>IMAGE URL</li>
          <li> <input v-model="img" required  type="text"></li>
          <li>Shoes<input v-model="category"  style="margin:10px;" type="radio">Accessories<input v-model="category" style="margin:10px;" type="radio">Clothing<input v-model="category" style="margin:10px;" type="radio"></li>
        </ul>

    
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
          <button type="submit" @click="createProduct" class="btn btn-success">Save changes</button>
 
       </form>
  </div>
</template>

<script>
export default {
data() {
    return {
      products: null,
      name:"",
      category:"",
      price:"",
      img:""

    };
  },
   // add product
    createProduct() {
      console.log(this.name, this.price, this.category, this.img) 
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
    }
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
</style>