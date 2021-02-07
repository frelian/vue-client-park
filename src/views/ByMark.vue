<template>

  <div>
    <br>
    <b-jumbotron header="Vehiculos" lead="Contador por marcas">
      <p>Cantidad de vehículos existentes por cada marca,
        donde se modifiquen los nombres de dichas marcas para que siempre se muestren
        únicamente con la primer letra en mayúscula y las demás en minúscula.</p>
    </b-jumbotron>

    <b-list-group>
      <b-list-group-item href="#" active>Listado de marcas y el total de cada una</b-list-group-item>
      <b-list-group-item
          v-for="vehicle in vehicles" v-bind:key="vehicle.id"
          class="d-flex justify-content-between align-items-center items-list">
        {{vehicle.mark}}
        <b-badge variant="primary" pill>{{vehicle.total}}</b-badge>
      </b-list-group-item>
    </b-list-group>
    <br>
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
        .get('https://gradiweb-server.herokuapp.com/api/vehicles/mark')
        .then(res => {
          // console.log(res.data.data);
          this.vehicles = res.data.data;
        })
  }
}
</script>

<style>
  .badge {
      font-size: 100%;
  }

  .items-list {
      font-size: 1.3em;
  }

  .items-list:hover {
    background-color: #dee2e6;
    font-weight: bolder;
    font-size: 1.5em;
  }

</style>