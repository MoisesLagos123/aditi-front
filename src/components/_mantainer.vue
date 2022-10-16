<template>
  <div>
    <b-table
      class="mt-3"
      :items="items"
      :fields="fields"
      responsive="sm"
      ref="selectableTable"
    >
    <template #cell(action)="row">
      <b-button size="sm" @click="showModal(row.item.group)"  variant="info">Ver</b-button>
    </template>
    </b-table>
    <b-modal 
      ref="my-modal" 
      hide-footer
      :id="infoModal.id" 
      :title="infoModal.title" 
      ok-only 
      @hide="resetInfoModal">
      <div class="d-block text-center">
      </div>
    </b-modal> 
  </div>
  
</template>

<script>
  export default {
    data() {
      return {
        fields: [
          { key: 'group', label: 'Grupo',},
          { key: 'action', label: 'Accion',},

        ],
        items: [
          { group:'Direcciones'},
          { group:'Clientes'},
          { group:'Modelos'},
        ],
        infoModal: {
            id: 'info-modal',
            title: '',
            content: ''
          }
      }
    },
    methods: {
      showModal(row) {
        this.infoModal.title = `Row index: ${row}`
        this.$refs['my-modal'].show()
      },
      resetInfoModal() {
          this.infoModal.title = ''
          this.infoModal.content = ''
        },

    }
  }
</script>