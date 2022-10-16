<template>
    <div class="about">
  
      <h1 class="mt-5">Mantenedor</h1>
      <b-row class="row justify-content-center">
        <b-col lg="5">
          <b-card class="m-5" >
            <Mantainer></Mantainer>
          </b-card>
        </b-col>
      </b-row>

  
    </div>
  </template>
  <script>
  // @ is an alias to /src
  import Mantainer from '@/components/_mantainer.vue'
  
  export default {
    name: 'HomeView',
    components: {
        Mantainer
    }
  }
  </script>