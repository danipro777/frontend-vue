<template>
  <b-container fluid>
    <b-modal id="modal-1" ref="modal-1" size="xl" title="Ingreso de tenis">
      <form>
        <!--Div de Name-->
        <div class="col-md-12 mb-3">
          <label for="name">Name</label>
          <input
            required
            type="text"
            class="form-control"
            id="name"
            v-model.trim="$v.form.name.$model"
            :state="!$v.form.name.$error"
            placeholder="Insert name"
          >
        </div>
        <!--Div de Size-->
        <div class="col-md-12 mb-3">
          <label for="size">Size</label>
          <input
            required
            class="form-control"
            id="size"
            v-model.trim="$v.form.size.$model"
            :state="!$v.form.size.$error"
            placeholder="Insert size"
          >
        </div>
        <!--Div de price-->
        <div class="col-md-12 mb-3">
          <label for="price">Price</label>
          <input
            required
            class="form-control"
            id="price"
            v-model.trim="$v.form.price.$model"
            :state="!$v.form.price.$error"
            placeholder="Insert price"
          >
        </div>
      </form>
      <template #modal-footer="{}">
        <b-button  variant="primary" @click="onSave()"
          >Guardar</b-button
        >
        <b-button variant="danger" @click="closeModal('save')"
          >Cancelar</b-button
        >
      </template>
    </b-modal>
    <b-modal id="modal-3" ref="modal-3" title="Desactivar especialidad">
      <h6 class="my-4">
        ¿Desea aumental la talla del producto: {{ form.name }} ?
      </h6>
      <template #modal-footer="{}">
        <b-button
          type="submit"
          variant="primary"
          @click="onState()
                  $bvModal.hide('modal-3')"
          >Aumemtar</b-button
        >
        <b-button variant="danger" @click="$bvModal.hide('modal-3')"
          >Cancelar</b-button
        >
      </template>
    </b-modal>
    <b-modal id="modal-4" ref="modal-4" title="Activar especialidad">
      <h6 class="my-4">
        ¿Desea reducir la talla del producto: {{ form.user }} ?
      </h6>
      <template #modal-footer="{}">
        <b-button
          type="submit"
          variant="primary"
          @click="onState()
                  $bvModal.hide('modal-4')"
          >Reducir</b-button
        >
        <b-button variant="danger" @click="$bvModal.hide('modal-4')"
          >Cancelar</b-button
        >
      </template>
    </b-modal>
    <b-modal id="modal-5" ref="modal-5" title="Activar especialidad">
      <h6 class="my-4">
        ¿Desea eliminar el registro?
      </h6>
      <template #modal-footer="{}">
        <b-button
          type="submit"
          variant="primary"
          @click="eliminarRegistro(form)
                  $bvModal.hide('modal-5')"
          >ELIMINAR</b-button
        >
        <b-button variant="danger" @click="$bvModal.hide('modal-5')"
          >Cancelar</b-button
        >
      </template>
    </b-modal>
    <b-row>
      <b-col md="12">
        <iq-card>
            <template v-slot:headerTitle>
              <h4 class="card-title mt-3">Alumnos</h4>
              <div class="iq-search-bar mt-2">
                <div class="row">
                  <div class="col-sm">
                    <b-form action="#" class="searchbox">
                        <b-input id="search" placeholder="Buscar..." @input="(val) => searchChange(val)" />
                        <a class="search-link" href="#"><i class="ri-search-line"></i></a>
                    </b-form>
                  </div>
                  <div class="col-sm">
                    <b-dropdown
                      id="ddown1"
                      :text="columna.nombre"
                      variant="outline-dark"
                      class="mr-1 float-md-left btn-group"
                      size="xs"
                    >
                      <b-dropdown-item
                        v-for="(search, index) in options"
                        :key="index"
                        @click="changeTypeSearch(search)"
                        >{{ search.nombre }}</b-dropdown-item
                      >
                    </b-dropdown>
                  </div>
                </div>
              </div>
            </template>
            <template v-slot:headerAction>
            <b-button variant="primary"  v-b-modal.modal-1>AGREGAR NUEVO</b-button>
          </template>
          <template v-slot:body>
            <table>
              <thead>
                <tr>
                  <th>Tipo</th>
                  <th>Nombre</th>
                  <th>Talla</th>
                  <th>Precio</th>
                  <th>Eliminar</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="datos in datosPosts" :key="datos.id">
                  <td>
                    <template v-if="datos.size < 40">
                      <button class="btn btn-success" @click="modificar(1, datos)">
                        AUMENTAR TALLA
                      </button>
                    </template>
                    <template v-else>
                      <button class="btn btn-danger" @click="modificar(2, datos)">
                        DISMINUIR TALLA
                      </button>
                    </template>
                  </td>
                  <td v-text="datos.name"></td>
                  <td v-text="datos.size"></td>
                  <td v-text="datos.price"></td>
                  <td><button class="btn btn-dark" @click="obtenerDatos(datos)">ELIMINAR</button></td>
                </tr>
              </tbody>
            </table>
          </template>
        </iq-card>
      </b-col>
    </b-row>
  </b-container>
</template>
<script>
import { xray } from '../../../config/pluginInit'
// import VuetablePagination from 'vuetable-2/src/components/VuetablePagination.vue'
import useVuelidate from '@vuelidate/core'
import { required } from '@vuelidate/validators'
import axios from 'axios'
import { apiUrl, laraverurl } from '../../../config/constant'

export default {
  name: 'Alumnos',
  components: {
  },
  setup () {
    return { $v: useVuelidate() }
  },
  mounted () {
    xray.index()
    axios.get(apiUrl + '/type/get').then((response) => {
      this.typeOptions = response.data
    })
    this.getDatos()
    console.log('Aqui ya esta montado el componente')
  },
  beforeDestroy () {
    // vacio
    this.mensajeDespedida()
  },
  beforeMount () {
    console.log('Aqui empieza el componente')
  },
  data () {
    return {
      from: 0,
      to: 0,
      total: 0,
      perPage: 5,
      search: '',
      datosPosts: [],
      form: {
        id: 0,
        name: '',
        size: '',
        price: ''
      },
      apiBase: laraverurl + '/sneackers/get',
      typeOptions: [],
      options: [
        { value: '1', nombre: 'name' },
        { value: '2', nombre: 'size' },
        { value: '3', nombre: 'price' }
      ],
      columna: { value: '1', nombre: 'Buscar' },
      fields: [
        {
          name: '__slot:actions',
          title: 'Acciones',
          titleClass: '',
          dataClass: 'text-muted'
          // width: "15%",
        },
        {
          name: 'name',
          sortField: 'name',
          title: 'Name',
          dataClass: 'list-item-heading'
        },
        {
          name: 'size',
          sortField: 'size',
          title: 'Size',
          dataClass: 'list-item-heading'
        },
        {
          name: 'price',
          sortField: 'price',
          title: 'Price',
          dataClass: 'list-item-heading'
        },
        {
          name: '__slot:estado',
          title: 'Estado',
          titleClass: '',
          dataClass: 'text-muted',
          width: '25%'
        }
      ]
    }
  },
  validations () {
    return {
      form: {
        name: { required },
        size: { required },
        price: { required }
      }
    }
  },
  methods: {
    eliminarRegistro (datos) {
      axios.delete(laraverurl + '/sneackers/' + datos.id).then((response) => {
        console.log('Eliminado')
        this.getDatos()
      })
    },
    obtenerDatos (datos) {
      this.form = datos
      this.form.name = datos.name
      this.$refs['modal-5'].show()
    },
    getDatos () {
      axios.get(laraverurl + '/sneackers/get').then((response) => {
        this.datosPosts = response.data
        console.log(this.datosPosts)
      })
    },
    openModal (modal, action) {
      switch (modal) {
        case 'save': {
          this.$v.$reset()
          this.form.id = 0
          this.form.name = ''
          this.form.size = ''
          this.form.price = ''
          break
        }
      }
    },
    closeModal (action) {
      switch (action) {
        case 'save': {
          this.$v.$reset()
          this.$refs['modal-1'].hide()
          this.form.id = 0
          this.form.name = ''
          this.form.size = ''
          this.form.price = ''
          break
        }
        case 'update': {
          this.$v.$reset()
          this.$refs['modal-2'].hide()
          this.form.id = 0
          this.form.name = ''
          this.form.size = ''
          this.form.price = ''
          break
        }
      }
    },
    onValidate (action) {
      this.$v.$touch()
      if (this.$v.$error !== true) {
        if (action === 'save') {
          this.onSave()
        } else if (action === 'update') {
          this.onUpdate()
        }
      }
    },
    setData (data) {
      this.form.name = data.name
      this.form.size = data.size
      this.form.price = data.price
      this.form.id = data.id
    },
    /* Guardar */
    onSave () {
      const me = this
      axios.post(laraverurl + '/sneackers/', {
        name: me.form.name,
        size: me.form.size,
        price: me.form.price })
        .then((response) => {
          me.getDatos()
          me.closeModal('save')
        })
        .catch((error) => {
          console.error('Error!', error)
        })
    },
    /* Guardar */
    onUpdate () {
      const me = this
      axios.put(apiUrl + '/user/update', {
        form: me.form })
        .then((response) => {
          me.closeModal('update')
        })
        .catch((error) => {
          console.error('Error!', error)
        })
    },
    onState () {
      let me = this
      if (this.form.size < 40) {
        axios
          .put(laraverurl + '/sneackers/sumSize/' + parseInt(this.form.id), {
            id: this.form.id
          })
          .then((response) => {
            me.$refs['modal-3'].hide()
          })
          .catch((error) => {
            console.error('There was an error!', error)
          })
      } else {
        axios
          .put(laraverurl + '/sneackers/resSize/' + parseInt(this.form.id), {
            id: this.form.id
          })
          .then((response) => {
            me.$refs['modal-4'].hide()
          })
          .catch((error) => {
            // this.errorMessage = error.message;
            console.error('There was an error!', error)
          })
      }
    },
    makeQueryParams (sortOrder, currentPage, perPage) {
      return sortOrder[0]
        ? {
          criterio: sortOrder[0] ? sortOrder[0].sortField : 'createdAt',
          order: sortOrder[0] ? sortOrder[0].direction : 'desc',
          page: currentPage,
          limit: this.perPage,
          search: this.search,
          columna: this.columna.value
        }
        : {
          criterio: sortOrder[0] ? sortOrder[0].sortField : 'createdAt',
          order: sortOrder[0] ? sortOrder[0].direction : 'desc',
          page: currentPage,
          limit: this.perPage,
          search: this.search,
          columna: this.columna.value
        }
    },
    changePageSizes (perPage) {
      this.perPage = perPage
      this.$refs.vuetable.refresh()
    },
    searchChange (val) {
      this.search = val.toLowerCase()
      this.$refs.vuetable.refresh()
    },
    onPaginationData (paginationData) {
      this.from = paginationData.from
      this.to = paginationData.to
      this.total = paginationData.total
      this.lastPage = paginationData.last_page
      this.items = paginationData.data
      this.$refs.pagination.setPaginationData(paginationData)
    },
    onChangePage (page) {
      this.$refs.vuetable.changePage(page)
    },
    changeTypeSearch (columna) {
      this.columna = columna
    },
    mensaje (mensaje) {
      this.form.mensaje = mensaje
    },
    mensajeDespedida () {
      console.log('Antes de irnos del componente manda este mensaje')
    },
    modificar (accion, datos) {
      this.form.name = datos.name
      this.form.size = datos.size
      this.form.id = datos.id
      if (accion === 1) {
        this.mensaje('Este calzado es para adultos')
        this.$refs['modal-3'].show()
      } else if (accion === 2) {
        this.mensaje('Este calzado es para niños')
        this.$refs['modal-4'].show()
      }
    }
  }
}
</script>
