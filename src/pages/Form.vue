<template>
  <q-page padding>
    <h1>Form</h1>
    <q-form
      class="row q-col-gutter-md"
      @submit.prevent="procesarFormulario"
      @reset="reset"
      ref="myForm"
      >
      <div class="col-12 col-sm-6">
         <q-input
           label="Producto"
           v-model="producto"
           lazy-rules
           :rules="[ val => val && val.length > 0 || 'Please type something']"
           />
      </div>
      <div class="col-12 col-sm-6">
        <q-select
          label="Prioridad"
          v-model="select"
          :options="option"
          lazy-rules
          :rules="[ val => val && val.length > 0 || 'Please type something']"
        />
      </div>
      <div class="col-12">
        <q-toggle
          v-model="accept"
          label="I accept the license and terms" />
      </div>
      <div class="col-12">
        <q-btn
          color="primary"
          label="Submit"
          type="submit"/>
        <q-btn
          color="primary"
          label="Reset"
          outline
          class="q-ml-sm"
          :ripple="false"
          type="reset"
          />
      </div>
    </q-form>
    <Table
      :productos = "productos"
    />
  </q-page>
</template>

<script>
import { ref } from 'vue'
import { useQuasar } from 'quasar'
import Table from '../components/Table.vue'
export default {
  components: {
    Table
  },
  setup () {
    const $q = useQuasar()
    // hace referencia al formulaio compelto
    const myForm = ref(null)
    const producto = ref(null)
    const select = ref(null)
    const option = ['minima', 'maxima', 'normal']
    const accept = ref(false)
    let productos = ref([])
    const procesarFormulario = () => {
      if (!accept.value) {
        $q.notify({
          color: 'red-5',
          textColor: 'white',
          icon: 'warning',
          message: 'You need to accept the license and terms first'
        })
      } else {
        $q.notify({
          color: 'green-4',
          textColor: 'white',
          icon: 'cloud_done',
          message: 'Submitted'
        })
        // nos permite borrar el formulario
        myForm.value.resetValidation()

        productos = [...productos.value, {
          producto: producto.value,
          prioridad: select.value
        }]
        reset()
      }
      console.log('me diste un click')
    }
    const reset = () => {
      producto.value = null
      select.value = null
      accept.value = false
    }
    return {
      producto,
      select,
      option,
      procesarFormulario,
      accept,
      reset,
      myForm,
      productos
    }
  }
}
</script>
