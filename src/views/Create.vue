<template>
  <div>
    <br>
    <div>
      <b-jumbotron header="Nuevo vehiculo" lead="Formulario">
        <p>* Todos los campos son obligatorios</p>
      </b-jumbotron>
    </div>
    <section v-if="errored">
      <b-alert variant="danger" show>Lo siento, no se pudo registrar el nuevo usuario. {{ error_info }}</b-alert>
    </section>
    <section v-if="ok">
      <b-alert variant="success" show>Nuevo usuario y su vehiculo registrado correctamente !</b-alert>
    </section>

    <b-form @submit="onSubmit" @reset="onReset" v-if="show">

      <b-form-group id="input-group-1" label="Nombre del usuario:" label-for="input-names">
        <b-form-input
            id="input-names"
            v-model="form.names"
            placeholder="Nombre"
            required>
        </b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Cédula de ciudadanía:" label-for="input-ide">
        <b-form-input
            id="input-ide"
            v-model="form.identification"
            placeholder="CC"
            required>
        </b-form-input>
      </b-form-group>

      <b-form-group
          id="input-group-3"
          label="Email address:"
          label-for="input-email">
        <b-form-input
            id="input-email"
            v-model="form.email"
            type="email"
            placeholder="Email"
            required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-4" label="Placa:" label-for="input-plate">
        <b-form-input
            id="input-plate"
            v-model="form.plate"
            placeholder="Placa del vehiculo"
            required
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-5" label="Marca:" label-for="input-mark">
        <b-form-input
            id="input-mark"
            v-model="form.mark"
            placeholder="Marca del vehiculo"
            required
        ></b-form-input>
      </b-form-group>


      <b-form-group id="input-group-6" label="Tipo:" label-for="input-type">
        <b-form-select
            id="input-type"
            v-model="form.type"
            :options="types"
            required
        ></b-form-select>
      </b-form-group>

      <b-button type="submit" variant="primary">Guardar</b-button>
      <b-button type="reset" variant="danger">Limpiar</b-button>
    </b-form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      form: {
        names: '',
        identification: '',
        email: '',
        plate: '',
        mark: '',
        type: null,
      },
      types: [
          { text: 'Seleccione', value: null },
          { text: 'Motocicleta', value: "motocicleta" },
          { text: 'Motocarro', value: "motocarro" },
          { text: 'Automóvil', value: "automovil" },
          { text: 'Campero', value: "campero" },
          { text: 'Camioneta', value: "camioneta" },
        ],
      show: true,
      errored: false,
      ok: false,
      error_info: '',
    }
  },
  methods: {
    onSubmit(event) {
      event.preventDefault()
      const data = {
        "names": this.form.mark,
        "identification": this.form.identification,
        "email": this.form.email,
        "plate": this.form.plate,
        "mark": this.form.mark,
        "type": this.form.type,
      }

      axios
          .post('http://127.0.0.1:8000/api/vehicles/store', data)
          .then(res => {
              console.log(res)
              this.ok = true
              this.errored = false
              this.identification = ''
              event.target.reset()
          })
          .catch(error => {
              console.log(error)
              this.errored = true
              this.ok = false
              this.error_info = error
          })
    },
    onReset(event) {
      event.preventDefault()
      this.form.names = ''
      this.identification = ''
      this.form.email = ''
      this.form.plate = ''
      this.form.mark = ''
      this.form.type = null

      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    }
  }
}
</script>