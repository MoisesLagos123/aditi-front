<template>
  <div id="app">
    <b-navbar class="b-navBar" toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="/">ADITI</b-navbar-brand>
  
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
  
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="#/AdministrarInventario/">Administrar Inventario</b-nav-item>
          <b-nav-item href="#">Mantenedor</b-nav-item>
          <b-nav-item href="#">Informes Web</b-nav-item>
          <b-nav-item href="#">Importación Masiva</b-nav-item>
          <b-nav-item href="#">Fallas</b-nav-item>



        </b-navbar-nav>
  
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <b-form-input size="sm" class="mr-sm-2" placeholder="Buscar en Inventario"></b-form-input>
            <b-button size="sm" class="my-2 my-sm-0" type="submit">Buscar</b-button>
          </b-nav-form>

          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template #button-content>
              <em>USR</em>
            </template>
            <b-dropdown-item href="#">Perfil</b-dropdown-item>
            <b-dropdown-item href="#">Desconectar</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <router-view/>
  </div>
</template>

<script>
export default {
  created () {
    document.body.style.backgroundColor = '#ececec'
  },
  data: () => ({
  })

}
</script>

<style>
.b-navBar {
  background-color: #15658d !important;
}
#app {
  position:unset;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
