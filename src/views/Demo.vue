<template>
  <div class="about justify-content-center">
    <br>
    <h1>Demo</h1>
    <br>
    <p class="justify-content">En una parte de la UI, queremos mostrarle a nuestro cliente un DEMO de una nueva
      funcionalidad, para ello se debe construir una función JS que recibe un arreglo con un
      conjunto de arreglos, y debe agrupar en el primer nivel por la fecha y en el segundo nivel
      con la franja horaria.
    </p>

    <b-form @submit="onSubmit" @reset="onReset">

      <b-form-group id="input-group-1" label="Clic para ejecutar y obtener el objeto:">
        <pre class="mt-3 mb-0">{{ arrayField }}</pre>
      </b-form-group>

      <b-button type="submit" variant="primary">Ejecutar</b-button>
    </b-form>

    <br>
    <b-card class="mt-3" header="Objeto resultante:">
      <pre class="m-0">{{ result }}</pre>
    </b-card>

  </div>
</template>

<script>

export default {
  data() {
    return {
      arrayField: '',
      result: '',
    }
  },
  methods: {
    onSubmit(event) {

      let array = [["2018-12-01","AM","ID123",5000],["2018-12-01","AM","ID545",7000],["2018-12-01","PM","ID545",3000],["2018-12-02","AM","ID545",7000]];

      /*
            [
                ["2018-12-01","AM","ID123",5000],
                ["2018-12-01","AM","ID545",7000],
                ["2018-12-01","PM","ID545",3000],
                ["2018-12-02","AM","ID545",7000]
            ]
       */

      let buscaFecha1   = array.filter(n => n[0] == "2018-12-01");
      let buscaFecha2   = array.filter(n => n[0] == "2018-12-02");
      let buscaAm1  = buscaFecha1.filter(n => n[1] == "AM");
      let buscaAm2  = buscaFecha2.filter(n => n[1] == "AM");

      let buscaPm1 = buscaFecha1.filter(n => n[1] == "PM");
      let buscaPm2 = buscaFecha2.filter(n => n[1] == "PM");

      let sumaAm1 = 0;
      for (var i = 0; i < buscaAm1.length; i++ ) {
         sumaAm1 += buscaAm1[i][3];
      }

      let sumaAm2 = 0;
      for (var i = 0; i < buscaAm2.length; i++ ) {
        sumaAm2 += buscaAm2[i][3];
      }

      let sumaPm1 = 0;
      for (var i = 0; i < buscaPm1.length; i++ ) {
        sumaPm1 += buscaPm1[i][3];
      }

      let sumaPm2 = 0;
      for (var i = 0; i < buscaPm2.length; i++ ) {
        sumaPm2 += buscaPm2[i][3];
      }

      let fecha1 = buscaFecha1[0][0];
      let fecha2 = buscaFecha2[0][0];
      let am = buscaFecha1[0][1];
      let pm = buscaFecha1[2][1];

      // Armar el objeto
      let objetoString =
      '{' +
        '"' + fecha1 + '": {' +
            '"' + am + '":"' + sumaAm1 + '",' +
            '"' + pm + '":"' + sumaPm1 + '"' +
          '},' +
        '"' + fecha2 + '": {' +
            '"' + am + '":"' + sumaAm2 + '"' +
        '}}';

      var miObj = JSON.parse(objetoString.toString());
      this.result = miObj;

      event.preventDefault()
      const data = {
        "data": this.arrayField,
      }

    },
    onReset(event) {
      event.preventDefault()
      this.arrayField = ''
    }
  }
}
</script>
