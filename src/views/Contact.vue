<template>
  <h1>Contact</h1>
<form @submit.prevent="handleSubmit">
              <br>
               <input name="fname" type="text" placeholder="Name" v-model="name" required>
                <input name="email" type="email" placeholder="Email" v-model="email" required> 

            <textarea name="messages" id="areatxt" cols="30" rows="8"
                  placeholder="Type your message" v-model="message" required></textarea> 
              <div style="display:flex"> 
                <button class="send-but buttunz" type="submit">Send</button>
                <button  class=" buttunz" type="reset" value="Reset">Reset</button>
              </div>
              <p>{{success}}</p>
            </form>

  
</template>


<script>
export default {
  data(){
    return{
  name:"",
  email:"",
  message:"",
  success:''
    }

  },
  methods:{
    handleSubmit(){
      fetch('https://contact2627.herokuapp.com/contact', {
  method: 'POST',
  body: JSON.stringify({
    name: this.name,
  email: this.email,
    message: this.message
  }),
  headers: {
    'Content-type': 'application/json; charset=UTF-8',
  },
})
  .then((response) => response.json())

  .then((json) => {
    console.log(json)
    console.log(json.msg)
    this.success = json.msg; 
    this.name = '',
    this.email = '',
    this.message = ''
  });
    }
  }


}

</script>

<style scoped>
input{
    width: 100%;
}
</style>