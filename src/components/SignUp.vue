<template>
    <div>
        <img class="logo" src="../assets/logo.png">
        <h1>Sign Up</h1>
        <div class="register">
            <input type="text" v-model="name" placeholder="Name">
            <input type="text" v-model="email" placeholder="Email">
            <input type="password" v-model="password" placeholder="Password">
            <button v-on:click="signUp" class="signup-button">Sign Up</button>
            <p>
                <router-link to="/login" class="login-link">Login</router-link>
            </p>
        </div>
    </div>
</template>
  
<script>
import axios from 'axios';

export default {
    name: 'SignUp',
    data() {
        return {
            name: '',
            email: '',
            password: '',
        };
    },
    methods: {
        async signUp() {
            let result = await axios.post("http://localhost:3000/user", {
                email: this.email,
                password: this.password,
                name: this.name
            });

            console.warn(result);
            if (result.status == 201) {
                localStorage.setItem("user-info", JSON.stringify(result.data));
                this.$router.push({ name: 'Home' });
            }
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (user) {
            this.$router.push({ name: 'Home' });
        }
    }
};
</script>
  
<style>
.register {
    text-align: center;
    margin-top: 20px;
}

.signup-button {
    background-color: #3498db;
    color: #fff;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 16px;
}

.signup-button:hover {
    background-color: #2980b9;
}

.login-link {
    color: #3498db;
    text-decoration: none;
    font-weight: bold;
    margin-top: 10px;
    display: inline-block;
}

.login-link:hover {
    color: #2980b9;
}
</style>