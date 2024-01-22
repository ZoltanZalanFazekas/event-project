<template>
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="/add">Add Event</router-link>
        <a v-on:click="logout" href="#">Logout</a>
    </div>
</template>

<script>
export default{
    name:'HeaderView',
    methods:{
        logout(){
            localStorage.clear();
            this.$router.push({name:'Login'})
        }
    }
}
</script>

<style>
.nav{
    background-color: skyblue;
    overflow: hidden;
    height: 50px;
}
.nav a{
    float: left;
    height: 30px;
    color: #f2f2f2;
    padding: 14px 14px;
    text-align: center;
    font-size: 17px;
    text-decoration: none;
    margin-right: 5px;
}
.nav a:hover{
    background: #ddd;
    color: #333;
}
</style>