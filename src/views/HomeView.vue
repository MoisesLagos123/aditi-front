<template>
  <div class="home">
    <img class="mt-5 mb-5" alt="Vue logo" src="../assets/logoPC.png">
    <WelcomeMessage msg="Bienvenido a ADITI" subMsg="Su gestor de inventario TI"/>
  </div>
</template>

<script>
// @ is an alias to /src
import WelcomeMessage from '@/components/WelcomeMessage.vue'

export default {
  name: 'HomeView',
  components: {
    WelcomeMessage
  }
}
</script>
