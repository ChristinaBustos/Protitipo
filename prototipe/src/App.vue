<template>
  <div id="app">
    <div>
  <b-navbar toggleable="lg" type="dark" class="bgprimary">
    <b-navbar-brand href="/">SGC | Sistema de Gestión de Capacitaciones</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item href="/about">Link</b-nav-item>
        <b-nav-item href="#" disabled>Disabled</b-nav-item>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <b-nav-item-dropdown right>
          <!-- Using 'button-content' slot -->
          <template #button-content>
            <em>Perfil</em>
          </template>
          <b-dropdown-item>Nombre completo usuario</b-dropdown-item>
          <b-dropdown-item href="#">Ver perfil</b-dropdown-item>
        </b-nav-item-dropdown>
        <b-button size="sm" class="bgsecondary">Salir</b-button>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</div>
    <router-view/>
  </div>
</template>

<style>
#app {
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

.bgprimary{
  background-color: #002E60;
}

.bgsecondary{
  background-color: #00AD8A;
}
</style>
