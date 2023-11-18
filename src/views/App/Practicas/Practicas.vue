<template>
    <b-container>
      <!-- ... (código existente) -->
      <form @submit.prevent="encriptarTexto">
        <div class="mb-3">
          <label for="texto" class="form-label">INGRESE TEXTO</label>
          <input type="text" v-model="texto" class="form-control" id="texto" aria-describedby="emailHelp">
        </div>
        <button type="submit" class="btn btn-primary">Encriptar</button>
      </form>
      <table class="table">
        <thead>
          <tr>
            <th scope="col">MD5</th>
            <th scope="col">SHA512</th>
            <!-- Otros encabezados -->
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>{{ md5Hash }}</td>
            <td>{{ sha512Hash }}</td>
            <!-- Otras celdas para otros hashes -->
          </tr>
        </tbody>
      </table>
    </b-container>
</template>
<script>
import { xray } from '../../../config/pluginInit'
// import axios from 'axios'
import useVuelidate from '@vuelidate/core'
// import { required } from '@vuelidate/validators'
// import { laraverurl } from '../../../config/constant'

export default {
  name: 'Ejercicio',
  setup () {
    return { $v: useVuelidate() }
  },
  components: {
  },
  data () {
    return {
      texto: '', // Guarda el texto ingresado
      md5Hash: '', // Guardará el hash MD5
      sha512Hash: '' // Guardará el hash SHA512
      // Otras variables para otros hashes
    }
  },
  mounted () {
    this.bienvenida()
    xray.index()
  },
  beforeMount () {
  },
  validations () {
  },
  methods: {
    bienvenida () {
      this.$refs['modal-3'].show()
    }
  }
}
</script>
