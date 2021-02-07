<template>
  <div id="app">

      <b-nav pills class="justify-content-center mt-5">
        <b-nav-item :to="{name:'Home'}" exact exact-active-class="active">Inicio</b-nav-item>
        <b-nav-item :to="{name:'Users'}" exact exact-active-class="active">Usuarios</b-nav-item>
        <b-nav-item :to="{name:'Vehicles'}" exact exact-active-class="active">Vehiculos</b-nav-item>
        <b-nav-item :to="{name:'Create'}" exact exact-active-class="active">Registrar Vehiculo</b-nav-item>
        <b-nav-item :to="{name:'Mark'}" exact exact-active-class="active">Vehiculos por marca</b-nav-item>
        <b-nav-item :to="{name:'Demo'}" exact exact-active-class="active">DEMO</b-nav-item>
      </b-nav>

    <b-container>
        <router-view/>
    </b-container>
  </div>
</template>