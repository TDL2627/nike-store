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

<div class="boxxie"  v-for="user of users" :key="user.name" >
  
<h1>{{user.name}}</h1>
<img :src="user.img" alt="profile pic">
<p>{{user.email}}</p>
<p>{{user.contact}}</p>
<p>{{user.about}}</p>
</div>
  </div>



</template>

<script>
export default {
    data() {
    return {
      users: null,
      name:"",
      contact:"",
      email:"",
      avatar:""

    };
  },
mounted() {
    if (localStorage.getItem("jwt")) {
      fetch("https://nike-store-api.herokuapp.com/users", {
        method: "GET",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.users = json;
          this.users.forEach(async (user) => {
            await fetch(
              "https://nike-store-api.herokuapp.com/users/" + user._id,
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
               user._id = json.name;
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
    
  }
}
</script>

<style scoped>
.boxxie{
  border: 2px solid white;
}
.profile{
   padding-top: 7%;
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
  
  right: 5px;
}
</style>