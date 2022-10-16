<template>
    <b-container fluid>
      <!-- User Interface controls -->
      <b-row class="mb-3 row justify-content-center">
        <b-col lg="1">
          <b-button variant="success">Agregar</b-button>
        </b-col>
    
        <b-col lg="7" class="my-1">
          <b-form-group
            label="Filtrar"
            label-for="filter-input"
            label-cols-sm="3"
            label-align-sm="right"
            label-size="sm"
            class="mb-0"
          >
            <b-input-group size="sm">
              <b-form-input
                id="filter-input"
                v-model="filter"
                type="search"
                placeholder="Buscar"
              ></b-form-input>
  
              <b-input-group-append>
                <b-button :disabled="!filter" @click="filter = ''">Limpiar</b-button>
              </b-input-group-append>
            </b-input-group>
          </b-form-group>
        </b-col>
        <b-col lg="4" class="my-1">
          <b-form-group
            label="Ordenar"
            label-for="sort-by-select"
            label-cols-sm="3"
            label-align-sm="right"
            label-size="sm"
            class="mb-0"
            v-slot="{ ariaDescribedby }"
          >
            <b-input-group size="sm">
              <b-form-select
                id="sort-by-select"
                v-model="sortBy"
                :options="sortOptions"
                :aria-describedby="ariaDescribedby"
                class="w-75"
              >
                <template #first>
                  <option value="">-- Sin Orden --</option>
                </template>
              </b-form-select>
  
              <b-form-select
                v-model="sortDesc"
                :disabled="!sortBy"
                :aria-describedby="ariaDescribedby"
                size="sm"
                class="w-25"
              >
                <option :value="false">Asc</option>
                <option :value="true">Desc</option>
              </b-form-select>
            </b-input-group>
          </b-form-group>
        </b-col>
      </b-row>
  
      <!-- Main table element -->
      <b-table
        :items="items"
        :fields="fields"
        :current-page="currentPage"
        :per-page="perPage"
        :filter="filter"
        :filter-included-fields="filterOn"
        :sort-by.sync="sortBy"
        :sort-desc.sync="sortDesc"
        :sort-direction="sortDirection"
        stacked="md"
        show-empty
        small
        @filtered="onFiltered"
      >        
        <template #cell(ip)="row">
          <a :href="'http://'+row.value">{{row.value}}</a>
        </template>
      
        <template #cell(name)="row">
          {{ row.value.first }} {{ row.value.last }}
        </template>
  
        <template #cell(actions)="row">
          <b-button size="sm" @click="info(row.item, row.index, $event.target)" class="mr-1" variant="info">Mas Info</b-button>
        </template>
        <template #row-details="row">
          <b-card>
            <ul>
              <li v-for="(value, key) in row.item" :key="key">{{ key }}: {{ value }}</li>
            </ul>
          </b-card>
        </template>
      </b-table>
      <b-row>
        <b-col sm="7" md="12" class="my-1" id="colPageBar">
          <b-pagination
            id="paginationPageBar"
            v-model="currentPage"
            :total-rows="totalRows"
            :per-page="perPage"
            align="fill"
            size="sm"
            class="my-0"
          ></b-pagination>
        </b-col>
      </b-row>
      <!-- Info modal -->
      <b-modal :id="infoModal.id" :title="infoModal.title" ok-only @hide="resetInfoModal">
        <pre>{{ infoModal.content }}</pre>
      </b-modal>
    </b-container>
  </template>
  
  <script>
    export default {
      data() {
        return {
          items: [
            { isActive: true, model: 'Nitro 3600', serie: '06xbh1546', marca:'ACER', ip:'10.191.156.2', direccio: 'arturo pratt 199 local 2'},
            { isActive: false, model: 'asd 3600', serie: '06xbh1546', marca:'HP', ip:'10.191.156.3', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: '456 3600', serie: '06xbh1fgh', marca:'HP', ip:'10.191.156.4', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh1535', marca:'ACER', ip:'10.191.156.5', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: '66 3600', serie: '06xbh1534', marca:'HP', ip:'10.191.156.6', direccio: 'arturo pratt 199 local 2'},
            { isActive: false, model: 'Nitro 3600', serie: '06xbh13456', marca:'ACER', ip:'10.191.156.7', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh154567', marca:'ACER', ip:'10.191.156.8', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: '88 3600', serie: '06xbh154786', marca:'HP', ip:'10.191.156.9', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh154688', marca:'ACER', ip:'10.191.156.10', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh15468888', marca:'ACER', ip:'10.191.156.12', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh1546', marca:'ACER', ip:'10.191.156.2', direccio: 'arturo pratt 199 local 2'},
            { isActive: false, model: 'asd 3600', serie: '06xbh1546', marca:'HP', ip:'10.191.156.3', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: '456 3600', serie: '06xbh1fgh', marca:'HP', ip:'10.191.156.4', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh1535', marca:'ACER', ip:'10.191.156.5', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: '66 3600', serie: '06xbh1534', marca:'HP', ip:'10.191.156.6', direccio: 'arturo pratt 199 local 2'},
            { isActive: false, model: 'Nitro 3600', serie: '06xbh13456', marca:'ACER', ip:'10.191.156.7', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh154567', marca:'ACER', ip:'10.191.156.8', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: '88 3600', serie: '06xbh154786', marca:'HP', ip:'10.191.156.9', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh154688', marca:'ACER', ip:'10.191.156.10', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh15468888', marca:'ACER', ip:'10.191.156.12', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh1546', marca:'ACER', ip:'10.191.156.2', direccio: 'arturo pratt 199 local 2'},
            { isActive: false, model: 'asd 3600', serie: '06xbh1546', marca:'HP', ip:'10.191.156.3', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: '456 3600', serie: '06xbh1fgh', marca:'HP', ip:'10.191.156.4', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh1535', marca:'ACER', ip:'10.191.156.5', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: '66 3600', serie: '06xbh1534', marca:'HP', ip:'10.191.156.6', direccio: 'arturo pratt 199 local 2'},
            { isActive: false, model: 'Nitro 3600', serie: '06xbh13456', marca:'ACER', ip:'10.191.156.7', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh154567', marca:'ACER', ip:'10.191.156.8', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: '88 3600', serie: '06xbh154786', marca:'HP', ip:'10.191.156.9', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh154688', marca:'ACER', ip:'10.191.156.10', direccio: 'arturo pratt 199 local 2'},
            { isActive: true, model: 'Nitro 3600', serie: '06xbh15468888', marca:'ACER', ip:'10.191.156.12', direccio: 'arturo pratt 199 local 2'},
          ],
          fields: [
            { key: 'marca', label: 'Marca', sortable: true, sortDirection: 'desc' },
            { key: 'model', label: 'Modelo', sortable: true, class: 'text-center' },
            { key: 'serie', label: 'Serie', sortable: true, class: 'text-center' },
            { key: 'ip', label: 'IP', sortable: true, class: 'text-center' },
            
            { key: 'isActive',
              label: 'Estado',
              formatter: (value, /*key, item*/) => {
                return value ? 'Activo' : 'De Baja'
              },
              sortable: true,
              sortByFormatted: true,
              filterByFormatted: true
            },
            { key: 'actions', label: 'Detalle' }
          ],
          totalRows: 1,
          currentPage: 1,
          perPage: 13,
          pageOptions: [5, 10, 15, { value: 100, text: "Show a lot" }],
          sortBy: '',
          sortDesc: false,
          sortDirection: 'asc',
          filter: null,
          filterOn: [],
          infoModal: {
            id: 'info-modal',
            title: '',
            content: ''
          }
        }
      },
      computed: {
        sortOptions() {
          // Create an options list from our fields
          return this.fields
            .filter(f => f.sortable)
            .map(f => {
              return { text: f.label, value: f.key }
            })
        }
      },
      mounted() {
        // Set the initial number of items
        this.totalRows = this.items.length
      },
      methods: {
        info(item, index, button) {
          this.infoModal.title = `Row index: ${index}`
          this.infoModal.content = JSON.stringify(item, null, 2)
          this.$root.$emit('bv::show::modal', this.infoModal.id, button)
        },
        resetInfoModal() {
          this.infoModal.title = ''
          this.infoModal.content = ''
        },
        onFiltered(filteredItems) {
          // Trigger pagination to update the number of buttons/pages due to filtering
          this.totalRows = filteredItems.length
          this.currentPage = 1
        }
      }
    }
  </script>

  <style>
  #colPageBar {
    text-align:center;
  }
  #paginationPageBar {
    width:50%; margin:0px auto;
  }
  </style>