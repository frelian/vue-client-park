<template>
  <div class="table-responsive">
    <br>
    <b-row>
      <b-col cols="12">
        <h3 class="text-center">Usuarios registrados:</h3>
        <br>
      </b-col>
    </b-row>
    <table class="table mt-4 table-hover">
      <thead>
      <tr>
        <th scope="col">ID</th>
        <th scope="col">Identificación</th>
        <th scope="col">Nombres</th>
        <th scope="col">Email</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="user in users" v-bind:key="user.id">
        <th scope="row">{{user.id}}</th>
        <td>{{user.identification}}</td>
        <td>{{user.names}}</td>
        <td>{{user.email}}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Users',
  data() {
    return {
      users: null,
    };
  },
  created: function() {
    axios
        .get('http://127.0.0.1:8000/api/users')
        .then(res => {
          // console.log(res.data);
          this.users = res.data;
        })
  }
}
</script>