<template>
  <div class="table-responsive">
    <br>
    <b-row>
      <b-col cols="12">
        <h3 class="text-center">Vehiculos registrados:</h3>
        <br><br>
      </b-col>
    </b-row>

    <form inline v-on:submit.prevent="noop">
      <b-row>
        <b-col cols="12" md="6" lg="4">
            <input type="text" placeholder="Buscar" class="form-control" v-model="inputSearch" v-on:keyup="validateinputSearch" />
        </b-col>
        <b-col>
            <b-form-select
                id="input-type-search"
                v-model="searchType"
                :options="searchtypes"
                required
            ></b-form-select>

        </b-col>
        <b-col cols="12" md="6" lg="2">
            <button type="button" class="btn btn-primary" v-on:click="postinputSearch" >Buscar</button>
        </b-col>
      </b-row>
    </form>
    <br>
    <b-alert show>Puede utilizar el buscador, si no elige un parametro de busqueda (Placa/Nombre/# Cédula) por defecto buscara por nombre. </b-alert>

    <table class="table mt-4 table-hover">
      <thead>
      <tr>
        <th scope="col">ID</th>
        <th scope="col">Marca</th>
        <th scope="col">Placa</th>
        <th scope="col">Usuario</th>
        <th scope="col">Identificación</th>
        <th scope="col">Registro</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="vehicle in vehicles" v-bind:key="vehicle.id_vehicle">
        <th scope="row">{{vehicle.id_vehicle}}</th>
        <td>{{vehicle.mark}}</td>
        <td>{{vehicle.plate}}</td>
        <td>{{vehicle.names}}</td>
        <td>{{vehicle.identification}}</td>
        <td>{{vehicle.vehicles_created_at}}</td>
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
      keyword: '',
      inputSearch: '',
      searchType: '',
      searchtypes: [
        { text: 'Seleccione tipo', value: null },
        { text: 'Placa', value: "plate" },
        { text: 'Nombre', value: "names" },
        { text: 'Cédula del propietario', value: "identification" },
      ],
    };
  },
  created: function() {
    this.getResults()
  },
  watch: {
    keyword: function(newVal) {
      if (newVal.length > 2) {
        this.getResults();
      }
    }
  },
  methods: {

    validateinputSearch: function(e) {
      if (e.keyCode === 13 && this.inputSearch != '' ) {
          this.getResults()
      }
    },

    postinputSearch: function() {
      this.getResults()
    },

    noop () {
      // do nothing
    },

    getResults() {
      // alert(this.searchType);
      axios
          .get("http://127.0.0.1:8000/api/vehicles/list?search=" + this.inputSearch + '&type=' + this.searchType)
          .then(res => {
              // console.log(res.data.data);
              this.vehicles = res.data.data;
          })
    }
  }
}
</script>