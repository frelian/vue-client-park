<template>
  <div class="container">
    <h3>Vehiculos registrados:</h3>
    <table class="table">
      <thead>
      <tr>
        <th scope="col">Id</th>
        <th scope="col">Identificación</th>
        <th scope="col">Name</th>
        <th scope="col">Email</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="user in vehicles" v-bind:key="user.id">
        <th scope="row">{{user.id}}</th>
        <td>{{user.identification}}</td>
        <td>{{user.name}}</td>
        <td>{{user.email}}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Vehicles',
  data() {
    return {
      vehicles: null,
    };
  },
  created: function() {
    axios
        .get('https://gradiweb-server.herokuapp.com/api/users')
        .then(res => {
          this.vehicles = res.data;
        })
  }
}
</script>