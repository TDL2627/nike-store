<template>
  <div class="profile">
       <the-loader></the-loader>
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

<div class="boxxie"  v-for="user of users" :key="user._id" >
  
<h1>{{user.name}}</h1>
<img :src="user.img" class="pp" alt="profile-pic">
<!-- <img src="@/assets/person.png" class="profile-pic" alt="pp"> -->
<p>{{user.email}}</p>
<p>{{user.contact}}</p>
<p>{{user.about}}</p>
<div class="divvie d-flex" >
<button class="btn btn-danger butt">DELETE</button>

<button class="btn btn-secondary butt">EDIT</button>
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
      users: null,
      name:"",
      contact:"",
      email:"",
      avatar:"",
      about:""

    };
  },
mounted() {
    if (localStorage.getItem("jwt")) {
      fetch("https://nike-store-api.herokuapp.com/users"  , {
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
    
  },
  
}
</script>

<style scoped>
.boxxie{
  margin: 10px;
  border: 2px solid white;
}
.divvie{
  text-align: center;
  margin-left: 43%;
}
.butt{
  margin: 10px;
}

.profile{
   padding-top: 7%;
    height: 100vh;
   overflow-y: scroll;
}

h1,h5,h3{
  color:red;
}
p{
  color: white;
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