<template>
  <div>
    <Header></Header>
    <img class="logo" src="../assets/logo.png" alt="Logo">
    <h1>List of events</h1>
    <table class="table">
      <thead>
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th>Address</th>
          <th>Date</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in event" :key="item.id">
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.address }}</td>
          <td>{{ item.date }}</td>
          <td>
            <router-link :to="'/update/' + item.id">
              <button class="update-button">Update</button>
            </router-link>
            <button class="delete-button" @click="deleteEvent(item.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Header from './Header.vue';
import axios from 'axios';

export default {
  name: 'HomeView',
  data() {
    return {
      event: [],
    };
  },
  components: {
    Header,
  },
  methods: {
    async deleteEvent(id) {
      let result = await axios.delete('http://localhost:3000/event/' + id);
      console.warn(result);
      if (result.status == 200) {
        this.loadData();
      }
    },
    async loadData() {
      let user = localStorage.getItem('user-info');
      if (!user) {
        this.$router.push({ name: 'SignUp' });
      }
      let result = await axios.get('http://localhost:3000/event');
      console.warn(result);
      this.event = result.data;
    },
  },
  async mounted() {
    this.loadData();
  },
};
</script>

<style>
.table {
  width: 80%;
  margin: 20px auto;
  border-collapse: collapse;
  text-align: center;
}

.table th, .table td {
  border: 1px solid #ddd;
  padding: 10px;
}

.table th {
  background-color: #f2f2f2;
}

.table tbody tr:hover {
  background-color: #f5f5f5;
}

.update-button {
  background-color: #3498db;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  margin-right: 5px;
}

.delete-button {
  background-color: #e74c3c;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}
</style>
