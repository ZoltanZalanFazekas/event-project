<template>
    <Header></Header>
    <h1>Update an existing event</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Name of event" v-model="event.name">
        <input type="text" name="address" placeholder="Location of event" v-model="event.address">
        <input type="text" name="date" placeholder="Date of event" v-model="event.date">
        <button type="button" v-on:click="updateEvent">Update existing event</button>
    </form>
</template>

<script>
import Header from './Header.vue';
import axios from 'axios';
export default{
    name: 'UpdateView',
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
        async updateEvent(){
            const result =await axios.put('http://localhost:3000/event/'+this.$route.params.id,{
                name:this.event.name,
                address:this.event.address,
                date:this.event.date,
            })
            if(result.status==200)
            {
                this.$router.push({name:'Home'})
            }
        }
    },
    async mounted(){
        let user=localStorage.getItem('user-info');
        if(!user){
            this.$router.push({name:'SignUp'})
        }
        const result = await axios.get('http://localhost:3000/event/'+this.$route.params.id)
        console.warn(result.data)
        this.event=result.data
    }
}
</script>