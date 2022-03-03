<template>
<div class="register">
  <router-link style="margin:40px" to="/"><svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px"
width="50" height="50"
viewBox="0 0 172 172"
style=" fill:#000000;"><g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#cccccc"><path d="M86,3.61469c-0.7482,0 -1.49345,0.23731 -2.12985,0.71891l-79.12,61.75203c-1.4792,1.1696 -1.75413,3.33062 -0.58453,4.84422c1.1696,1.4792 3.33062,1.75413 4.84422,0.58453l4.75016,-3.70875v90.43437c0,1.892 1.548,3.44 3.44,3.44h48.16v-61.92h41.28v61.92h48.16c1.892,0 3.44,-1.548 3.44,-3.44v-90.43437l4.75015,3.70875c0.6536,0.4816 1.37305,0.72563 2.12985,0.72563c1.032,0 2.02638,-0.45015 2.71437,-1.31015c1.1696,-1.5136 0.89467,-3.67462 -0.58453,-4.84422l-79.12,-61.75203c-0.6364,-0.4816 -1.38165,-0.71891 -2.12985,-0.71891zM120.4,17.2v3.61469l20.64,16.09813v-19.71281z"></path></g></g></svg>
</router-link>

  <form @submit.prevent="register" class="form neu-border">
   
    <h2 class="form-heading">Register</h2>
      <p>{{msg}}</p>
    <input
      class="form-input neu-border-inset"
      type="text"
      v-model="name"
      placeholder="Name"
        required
    />
    <input
      class="form-input neu-border-inset"
      type="email"
      v-model="email"
        required
      placeholder="Email"
    />
    <input
      class="form-input neu-border-inset"
      type="text"
      v-model="contact"
      placeholder="Contact Number"
        required
    />
    <input
      class="form-input neu-border-inset"
      type="password"
      v-model="password"
      placeholder="Password"
      required
    />

 <input type="text" placeholder="IMG URL (not required)" v-model="avatar"    class="form-input neu-border-inset">
 <textarea placeholder="About yourself (not required)"  v-model="about" cols="30"    class="form-input neu-border-inset" rows="10"></textarea>
    <button type="submit" class="form-btn neu-border">Sign up</button>
   

    <p>
      Already registered
      <router-link :to="{ name: 'Login' }">Sign in</router-link>
    </p>
  </form>
</div>

</template>
<script>
export default {
  data() {
    return {
      name: "",
      email: "",
      contact: "",
      password: "",
      about:"",
      msg: '',
      avatar:""
    };
  },
  methods: {
    register() {
         fetch('https://nike-store-api.herokuapp.com/users', {
  method: 'POST',
  body: JSON.stringify({
    email:this.email,
    password:this.password,
    name:this.name,
    contact:this.contact,
    about:this.about,
    avatar:this.avatar
  }),
  headers: {
    'Content-type': 'application/json; charset=UTF-8',
  },
})
  .then((response) => response.json())
  .then((json) => console.log(json));
      this.msg = `${ this.name }  Registered Successfuly`;
       alert("Logging in...");
          this.$router.push({ name: "Products" });
    },
  },
};
</script>
<style>
.register{
  padding-top:2%;
  padding-bottom: 7%;
    height: 100vh;
   overflow-y: scroll;
}
.neu-border {
  border-radius: 30px;
background-color: rgb(167, 167, 167);
  box-shadow: 8px 8px 15px #e4e4e4, -8px -8px 15px #ffffff;
}
.neu-border-inset {
  border-radius: 30px;
background-color: white;
  box-shadow: inset 8px 8px 15px #e4e4e4, inset -8px -8px 15px #ffffff;
}

.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 40px;
  gap: 20px;
  width: 100%;
  max-width: 600px;
  margin-inline: auto;
  margin-top: 20px;
}

.form-heading {
  text-align: center;
  text-transform: uppercase;
}

.form-input,
.form-btn {
  border: none;
  outline: none;
  padding: 20px;
}

.form-btn {
  cursor: pointer;
  transition: all 0.1s linear;
}

.form-btn:hover {
  transform: scale(1.05);
}

.form-social-login {
  display: flex;
  justify-content: space-between;
}

.form-social-btn {
  width: 45%;
  color: #333;
}
li{
  list-style: none;
}

a,h2{
  color:red;
}
button{
  color: black;

}
button:hover{
  color: white;
  background-color:black;

  
}
@media only screen and (max-width: 500px) {
.register{
  padding-bottom: 15%;
}
}
</style>
