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
    <div class="navg">
         <router-link class="nav-link" to="/products">PRODUCTS</router-link>
            <router-link class="nav-link" to="/cart">CART</router-link>
            <router-link class="nav-link" to="/">LOG OUT</router-link>
    </div>

    </div>
  </div>
</nav>

<div class="boxxie"  v-for="user of users" :key="user._id" >
  
<h1>{{user.name}}</h1>
<img :src="user.avatar" class="pp" alt="profile-pic">
<!-- <img src="@/assets/person.png" class="profile-pic" alt="pp"> -->
        <h3>EMAIL</h3>
<p>{{user.email}}</p>
<h3>CONTACT</h3>
<p>{{user.contact}}</p>
<h3>ABOUT</h3>
<p>{{user.about}}</p>
<div class="divvie d-flex" >
<button class="btn btn-danger butt">DELETE</button>

<button type="button" class="btn btn-secondary" style="margin:10px;" data-bs-toggle="modal" data-bs-target="#exampleModal1">
  EDIT 
</button>
</div>


</div>


<!-- Modal for edit  profile -->
<div class="modal fade" id="exampleModal1" tabindex="-1" aria-labelledby="exampleModalLabel1" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">EDIT NIKE</h5>
        <p>(not working yet)</p>
        
        <button type="button" class="btn-close btn-danger" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
       <form @submit.prevent="updateProduct">
    <ul>
      <li>NAME</li>
      <li> <input v-model="name" required type="text"></li>
            <li>CONTACT</li>
      <li> <input v-model="contact" required type="text"></li>
      <li>EMAIL</li>
<li> <input v-model="email" required type="email"></li>
<li>IMAGE URL</li>
<li> <input v-model="avatar" required  type="text"></li>
      <li>ABOUT</li>
      <li> <textarea name="about" v-model="about" cols="30" rows="10"></textarea></li>

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
    padding-bottom: 7%;
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

.pp{
    border-radius: 50%;
    border: solid 2px red;
    object-fit: cover;
    height: 200px;
    width:200px;

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
.profile{
    padding-top: 15%;
    padding-bottom:15%;
}
.divvie{
  text-align: center;
  margin-left: 23%;
}
}
</style>