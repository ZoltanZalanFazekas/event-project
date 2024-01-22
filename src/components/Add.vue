<template>
    <Header></Header>
    <h1>Create a new event</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Name of event" v-model="event.name">
        <input type="text" name="address" placeholder="Location of event" v-model="event.address">
        <input type="text" name="date" placeholder="Date of event" v-model="event.date">
        <button type="button" v-on:click="addEvent">Add new event</button>
    </form>
</template>

<script>
import Header from './Header.vue';
import axios from 'axios';
export default{
    name: 'AddView',
    components:{
        Header
    },
    data(){
        return{
            event:{
                name:'',
                address:'',
                date:''
            }
        }
    },
    methods:{
       async addEvent(){
            console.warn(this.event)
            const result =await axios.post('http://localhost:3000/event',{
                name:this.event.name,
                address:this.event.address,
                date:this.event.date,
            })
            if(result.status==201)
            {
                this.$router.push({name:'Home'})
            }
            console.warn('result',result)
        }
    },
    mounted(){
        let user=localStorage.getItem('user-info');
        if(!user){
            this.$router.push({name:'SignUp'})
        }
    }
}
</script>