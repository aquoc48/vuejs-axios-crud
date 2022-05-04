<template>
    <div class="user-add">
        <h2>Add user</h2>
        <input type="text" v-model="name" /> <br />
        <input type="text" v-model="email" /> <br />

        <button @click="addUser">add</button>
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
      async addUser() {
      try {
        const user = await axios.post("https://jsonplaceholder.typicode.com/users", {name: this.name, email : this.email,} );
        console.log(user)
      } 
      catch(e) {console.log(e);}
    }
  },
}
</script>

<style>

</style>