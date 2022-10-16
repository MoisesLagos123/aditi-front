<template>
  <div class="about">

    <h1 class="mt-5">Inventario</h1>

    <b-card class="m-5" >
      <DeviceList></DeviceList>
    </b-card>

  </div>
</template>
<script>
// @ is an alias to /src
import DeviceList from '@/components/_deviceList.vue'

export default {
  name: 'HomeView',
  components: {
    DeviceList
  }
}
</script>