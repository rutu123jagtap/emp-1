<template>
  <img class="logo" src="../assets/th.jpg"/>
    <h1>Login</h1>
    <div class="login">
      <input type="text" v-model="email" placeholder="Enter Email:">
      <input type="text" v-model="password" placeholder="Enter Password:">
      <button v-on:click="login">Login</button>
      <p>
        <router-link to="/sign-up">SignUp</router-link>
      </p>
  
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Login',
    data(){
        return {
            email:'',
            password:''
        }
    },
    methods:{
        async login(){
            let result = await axios.get(
                `http://localhost:3030/users?email-${this.email}&password-${this.password}`
            )

            if(result.status==200 && result.data.length>0){
                  localStorage.setItem("user.info",JSON.stringify(result.data[0]))
                  this.$router.push({name: 'Home'})
              }
            }
        },
        mounted()
      {
        let user = localStorage.getItem('user.info');
        if(user)
        {
            this.$router.push({ name: 'Home' })
        }
      }
    
}
</script>

<style scoped>
.logo{
      width: 70px; 
      margin: 0%;
  }
  .register input{
      width: 300px;
      height: 40px;
      padding-left: 20px;
      display: block;
      margin-bottom: 30px;
      margin-left: auto;
      margin-right: auto;
      border: 1px solid skyblue;
  }
  
  .register button{
      width: 320px;
      height: 40px;
      border: 1px solid skyblue;
      color: #fff;
      background-color: skyblue;
      cursor: pointer
  }
  
</style>