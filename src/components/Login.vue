<template>
    <div>
      <img class="logo" src="../assets/logo.png">
      <h1>Login</h1>
      <div class="login">
        <input type="text" v-model="email" placeholder="Email">
        <input type="password" v-model="password" placeholder="Password">
        <button v-on:click="login" class="login-button">Login</button>
        <p>
          <router-link to="/sign-up" class="signup-link">Sign Up</router-link>
        </p>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'LoginView',
    data() {
      return {
        email: '',
        password: ''
      };
    },
    methods: {
      async login() {
        let result = await axios.get(`http://localhost:3000/user?email=${this.email}&password=${this.password}`);
        if (result.status == 200) {
          localStorage.setItem("user-info", JSON.stringify(result.data[0]));
          this.$router.push({ name: 'Home' });
        }
        console.warn(result);
      }
    }
  };
  </script>
  
  <style>
  .login {
    text-align: center;
    margin-top: 20px;
  }
  
  .login-button {
    background-color: #3498db;
    color: #fff;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 16px;
  }
  
  .login-button:hover {
    background-color: #2980b9;
  }
  
  .signup-link {
    color: #3498db;
    text-decoration: none;
    font-weight: bold;
    margin-top: 10px;
    display: inline-block;
  }
  
  .signup-link:hover {
    color: #2980b9;
  }
  </style>
  