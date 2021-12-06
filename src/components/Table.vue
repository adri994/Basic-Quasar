<template>
  <q-table
    class="q-mt-lg"
    title="Producto"
    no-data-label="Sin producto por mostrar"
    :columns="column"
  />
</template>

<script>
const column = [
  {
    name: 'producto',
    label: 'Producto',
    align: 'left',
    field: 'producto',
    sortable: true
  },
  {
    name: 'prioridad',
    label: 'Prioridad',
    align: 'left',
    field: 'prioridad',
    sortable: true
  }
]
export default {
  props: {
    productos: Array
  },
  setup () {
    return {
      column
    }
  }
}
</script>
