<template>
  <div class="about">
    <br>
    <h1>Administrar Inventario</h1>
    <br>
    <DeviceList></DeviceList>
  </div>
</template>
<script>
// @ is an alias to /src
import DeviceList from '@/components/DeviceList.vue'

export default {
  name: 'HomeView',
  components: {
    DeviceList
  }
}
</script>