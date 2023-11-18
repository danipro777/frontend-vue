<template>
    <b-container fluid>
        <b-row>
        <b-col md="12">
          <iq-card>
            <template v-slot:headerTitle>
              <h4 class="card-title mt-3">Libreria</h4>
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
                <b-tab title="Libreria" active>
                  <div class="d-flex justify-content-end mb-3">
                    <b-button variant="primary" v-b-modal.modal-1>AGREGAR NUEVO</b-button>
                  </div>
                  <table id="miTabla" class="display">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Nombre</th>
                            <th>Descripcion</th>
                            <th>Precio Publico</th>
                            <th>Precio costo</th>
                            <th>Acciones</th>
                        </tr>
                    </thead>
                    <tbody>
                      <tr v-for="datos in datosPost" :key="datos.id">
                          <td v-text="datos.id"></td>
                          <td v-text="datos.nombre"></td>
                          <td v-text="datos.descripcion"></td>
                          <td v-text="datos.preciopublico"></td>
                          <td v-text="datos.preciocosto"></td>
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
                    <label for="nombre">Nombre</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="nombre"
                        v-model.trim="$v.form.nombre.$model"
                        :state="!$v.form.nombre.$error"
                        placeholder="Nombre del libro"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="descripcion">Descripcion</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="descripcion"
                        v-model.trim="$v.form.descripcion.$model"
                        :state="!$v.form.descripcion.$error"
                        placeholder="descripcion"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="preciopublico">Precio venta</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="preciopublico"
                        v-model.trim="$v.form.preciopublico.$model"
                        :state="!$v.form.preciopublico.$error"
                        placeholder="Precio venta"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="name4">Precio compra</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="preciocosto"
                        v-model.trim="$v.form.preciocosto.$model"
                        :state="!$v.form.preciocosto.$error"
                        placeholder="Precio compra"
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
                    <label for="nombre">Nombre</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="nombre"
                        v-model.trim="$v.form.nombre.$model"
                        :state="!$v.form.nombre.$error"
                        placeholder="Nombre del libro"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="descripcion">Descripcion</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="descripcion"
                        v-model.trim="$v.form.descripcion.$model"
                        :state="!$v.form.descripcion.$error"
                        placeholder="descripcion"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="preciopublico">Precio venta</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="preciopublico"
                        v-model.trim="$v.form.preciopublico.$model"
                        :state="!$v.form.preciopublico.$error"
                        placeholder="Precio venta"
                    >
                </div>
                <div class="col-md-6 mb-3">
                    <label for="name4">Precio compra</label>
                    <input
                        required
                        type="text"
                        class="form-control"
                        id="preciocosto"
                        v-model.trim="$v.form.preciocosto.$model"
                        :state="!$v.form.preciocosto.$error"
                        placeholder="Precio compra"
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
        nombre: '',
        descripcion: '',
        preciopublico: '',
        preciocosto: ''
      },
      apiBase: laraverurl + '/librerias/get'
    }
  },
  mounted () {
    xray.index()
    axios.get(laraverurl + '/librerias/get').then((response) => {
      this.datosPost = response.data
    })
  },
  beforeMount () {
  },
  validations () {
    return {
      form: {
        nombre: { required },
        descripcion: { required },
        preciopublico: { required },
        preciocosto: { required }
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
      this.form.nombre = datos.nombre
      this.form.descripcion = datos.descripcion
      this.form.preciopublico = datos.preciopublico
      this.form.preciocosto = datos.preciocosto
      this.$refs['modal-2'].show()
    },
    modalActualizar (datos) {
      this.form = datos
      this.$bvModal.show('modal-2')
    },
    onUpdate () {
      const me = this
      axios.put(laraverurl + '/librerias/' + parseInt(me.form.id), {
        nombre: me.form.nombre,
        descripcion: me.form.descripcion,
        preciopublico: me.form.preciopublico,
        preciocosto: me.form.preciocosto })
        .then((response) => {
          me.refresh()
          me.getDatos()
        })
        .catch((error) => {
          console.error('Error!', error)
        })
    },
    refresh () {
      axios.get(laraverurl + '/librerias/get').then((response) => {
        this.datosPost = response.data
      })
    },
    eliminarRegistro (datos) {
      axios.delete(laraverurl + '/librerias/' + datos.id).then((response) => {
        console.log(datos.id)
        console.log('Eliminado')
        this.refresh()
        this.getDatos()
      })
    },
    getDatos () {
      axios.get(laraverurl + '/librerias/get').then((response) => {
        this.datosPost = response.data
      })
    },
    /* Guardar */
    onSave () {
      const me = this
      axios.post(laraverurl + '/librerias/', {
        nombre: me.form.nombre,
        descripcion: me.form.descripcion,
        preciopublico: me.form.preciopublico,
        preciocosto: me.form.preciocosto })
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
