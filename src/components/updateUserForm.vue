<template>
     <div class="user-update">
      <h2>update user</h2>

      <input type="text" v-model="user.name" /> <br/>
      <input type="text" v-model="user.email" /> <br/>

      <button @click="updateUser">update</button>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
    return {
      users: [],
      user: {},
      name: '',
      email: '',
    };
  },
  methods: {
      async updateUser() {
      try {
        const user = await axios.put(`https://jsonplaceholder.typicode.com/users/${this.user.id}`, {name: this.user.name, email:this.user.email,});
      console.log(user.data);
      alert("user updated!");
    } catch (e) {
      console.log(e);
    }
    }
  },
}
</script>

<style>

</style>