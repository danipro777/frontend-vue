<template>
    <b-container fluid>
        <b-row>
        <b-col md="12">
          <iq-card>
            <template v-slot:headerTitle>
              <h4 class="card-title mt-3">Apps</h4>
              <div class="iq-search-bar mt-2">
                <div class="row">
                  <div class="col-sm">
                    <b-form action="#" class="searchbox">
                    </b-form>
                  </div>
                  <div class="col-sm">
                  </div>
                </div>
              </div>
            </template>
            <template v-slot:body>
              <b-tabs>
                <b-tab title="Apps" active>
                  <div class="d-flex justify-content-end mb-3">
                    <b-button variant="primary" v-b-modal.modal-1>AGREGAR NUEVO</b-button>
                  </div>
                  <table id="miTabla" class="display">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>App 1</th>
                            <th>App 2</th>
                            <th>App 3</th>
                            <th>App 4</th>
                            <th>App 5</th>
                            <th>Acciones</th>
                        </tr>
                    </thead>
                    <tbody>
                      <tr v-for="datos in datosPost" :key="datos.id">
                          <td v-text="datos.id"></td>
                          <td v-text="datos.name1"></td>
                          <td v-text="datos.name2"></td>
                          <td v-text="datos.name3"></td>
                          <td v-text="datos.name4"></td>
                          <td v-text="datos.name5"></td>
                          <td><b-button variant="danger" @click="modalEliminar(datos)">ELIMINAR</b-button><b-button variant="primary" @click="setData(datos)">EDITAR</b-button></td>
                      </tr>
                    </tbody>
                </table>
                </b-tab>
              </b-tabs>
            </template>
          </iq-card>
        </b-col>
        </b-row>
        <b-modal id="modal-1" ref="modal-1" size="xl" title="Bienvenido al ingreso de Apps">
            <form>
            <div class="row">
                <div class="col-md-6 mb-3">
                    <label for="name1">App 1</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="name1"
                        v-model.trim="$v.form.name1.$model"
                        :state="!$v.form.name1.$error"
                        placeholder="Nombre de la App"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="name2">App 2</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="name2"
                        v-model.trim="$v.form.name2.$model"
                        :state="!$v.form.name2.$error"
                        placeholder="Nombre de la App"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="name3">App 3</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="name3"
                        v-model.trim="$v.form.name3.$model"
                        :state="!$v.form.name3.$error"
                        placeholder="Nombre de la App"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="name4">App 4</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="name4"
                        v-model.trim="$v.form.name4.$model"
                        :state="!$v.form.name4.$error"
                        placeholder="Nombre de la App"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="name5">App 5</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="name5"
                        v-model.trim="$v.form.name5.$model"
                        :state="!$v.form.name5.$error"
                        placeholder="Nombre de la App"
                    >
                </div>
            </div>
            </form>
            <template #modal-footer="{}">
            <b-button  variant="primary" @click="onSave(), $bvModal.hide('modal-1')"
                >Guardar</b-button
            >
            <b-button variant="danger" @click="$bvModal.hide('modal-1')"
                >Cancelar</b-button
            >
            </template>
        </b-modal>
        <b-modal id="modal-2" ref="modal-2" size="xl" title="Bienvenido al modal de edicion de equipo">
            <form>
            <div class="row">
                <div class="col-md-6 mb-3">
                    <label for="name1">App 1</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="name1"
                        v-model.trim="$v.form.name1.$model"
                        :state="!$v.form.name1.$error"
                        placeholder="Nombre de la App"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="name2">App 2</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="name2"
                        v-model.trim="$v.form.name2.$model"
                        :state="!$v.form.name2.$error"
                        placeholder="Nombre de la App"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="name3">App 3</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="name3"
                        v-model.trim="$v.form.name3.$model"
                        :state="!$v.form.name3.$error"
                        placeholder="Nombre de la App"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="name4">App 4</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="name4"
                        v-model.trim="$v.form.name4.$model"
                        :state="!$v.form.name4.$error"
                        placeholder="Nombre de la App"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="name5">App 5</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="name5"
                        v-model.trim="$v.form.name5.$model"
                        :state="!$v.form.name5.$error"
                        placeholder="Nombre de la App"
                    >
                </div>
            </div>
            </form>
            <template #modal-footer="{}">
            <b-button  variant="primary" @click="onUpdate(), $bvModal.hide('modal-2')"
                >Editar</b-button
            >
            <b-button variant="danger" @click="$bvModal.hide('modal-2')"
                >Cancelar</b-button
            >
            </template>
        </b-modal>
        <b-modal id="modal-3" ref="modal-3" title="Eliminar equipo">
            <h6 class="my-4">
            ¿Desea eliminar el registro?
            </h6>
            <template #modal-footer="{}">
            <b-button
                type="submit"
                variant="primary"
                @click="eliminarRegistro(datos), $bvModal.hide('modal-3')">Eliminar</b-button>
            <b-button variant="danger" @click="$bvModal.hide('modal-3')"
                >Cancelar</b-button
            >
            </template>
        </b-modal>
    </b-container>
</template>
<script>
import { xray } from '../../../config/pluginInit'
import axios from 'axios'
import useVuelidate from '@vuelidate/core'
import { required } from '@vuelidate/validators'
import { laraverurl } from '../../../config/constant'

export default {
  name: 'Ejercicio',
  setup () {
    return { $v: useVuelidate() }
  },
  components: {
  },
  data () {
    return {
      search: '',
      datosPost: [],
      form: {
        name1: '',
        name2: '',
        name3: '',
        name4: '',
        name5: ''
      },
      apiBase: laraverurl + '/apps/get'
    }
  },
  mounted () {
    xray.index()
    axios.get(laraverurl + '/apps/get').then((response) => {
      this.datosPost = response.data
    })
  },
  beforeMount () {
  },
  validations () {
    return {
      form: {
        name1: { required },
        name2: { required },
        name3: { required },
        name4: { required },
        name5: { required }
      }
    }
  },
  methods: {
    modalEliminar (datos) {
      this.datos = datos
      this.$refs['modal-3'].show()
    },
    setData (datos) {
      this.datos = datos
      this.form.id = datos.id
      this.form.name1 = datos.name1
      this.form.name2 = datos.name2
      this.form.name3 = datos.name3
      this.form.name4 = datos.name4
      this.form.name5 = datos.name5
      this.$refs['modal-2'].show()
    },
    modalActualizar (datos) {
      this.form = datos
      this.$bvModal.show('modal-2')
    },
    onUpdate () {
      const me = this
      axios.put(laraverurl + '/apps/' + parseInt(me.form.id), {
        name1: me.form.name1,
        name2: me.form.name2,
        name3: me.form.name3,
        name4: me.form.name4,
        name5: me.form.name5 })
        .then((response) => {
          me.refresh()
          me.getDatos()
        })
        .catch((error) => {
          console.error('Error!', error)
        })
    },
    refresh () {
      axios.get(laraverurl + '/apps/get').then((response) => {
        this.datosPost = response.data
      })
    },
    eliminarRegistro (datos) {
      axios.delete(laraverurl + '/apps/' + datos.id).then((response) => {
        console.log(datos.id)
        console.log('Eliminado')
        this.refresh()
        this.getDatos()
      })
    },
    getDatos () {
      axios.get(laraverurl + '/apps/get').then((response) => {
        this.datosPost = response.data
      })
    },
    /* Guardar */
    onSave () {
      const me = this
      axios.post(laraverurl + '/apps/', {
        name1: me.form.name1,
        name2: me.form.name2,
        name3: me.form.name3,
        name4: me.form.name4,
        name5: me.form.name5 })
        .then((response) => {
          me.getDatos()
          me.refresh()
        })
        .catch((error) => {
          console.error('Error!', error)
        })
    }
  }
}
</script>
<style>
    table {
        width: 100%;
        border-collapse: collapse;
    }
    /* Estilo para las celdas de encabezado */
    th {
        background-color: #f2f2f2;
    }
    /* Estilo para las celdas de datos */
    td, th {
        border: 1px solid #ddd;
        padding: 8px;
        text-align: left;
    }
</style>
