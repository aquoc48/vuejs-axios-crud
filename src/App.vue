<template>
  
  <div id="app">
    <keep-alive>
      <component v-bind:is="component"></component>
    </keep-alive>
    <button @click="component = 'add-user-form'">Show Add user form</button>
    <button @click="component = 'update-user-form'">Show update user form</button>

    <button class="btn" @click="getUsers">Get users</button> <br />

    <div class="users" v-for="user in users" :key="user.id">
      <h2>{{ user.name }}</h2>
      <p>{{ user.email }}</p>
      <button @click="editUser(user)">edit</button>
      <button @click="deleteUser(user.id)">Delete</button>
    </div>

    
  </div>
</template>

<script>
import axios from 'axios'
import addUserForm from './components/addUserForm'
import updateUserForm from './components/updateUserForm'


export default {
  name: 'App',
  components: {
    'add-user-form': addUserForm,
    'update-user-form': updateUserForm,
  },
  data() {
    return {
      users: [],
      user: {},
      name: '',
      email: '',
      component: 'add-user-form',
    };
  },
  methods: {

    async getUsers() {
      try {
        const users = await axios.get("https://jsonplaceholder.typicode.com/users");

        this.users = users.data;
      } 
      catch (e) {console.log(e);}
    },

    async editUser(user) {
      this.user.name =user.name;
      this.user.email =user.email;
      this.user.id =user.id;
    },

    async deleteUser(id) {
      let x = window.confirm('delete user?');

      if (x) {
        const user = await axios.delete(`https://jsonplaceholder.typicode.com/users/${id}`);
        console.log(user);
        alert("user deleted");
      }
    },


  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
