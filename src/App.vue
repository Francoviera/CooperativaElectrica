<template>
  <ion-app id="app">
    <ion-menu side="start" menu-id="first" content-id="main">
      <ion-content>
        <div class="menu-header">
        </div>
        <div class="header-content">
          <img class="avatar-male" src="./assets/avatar-male.png" alt="">
          <ion-label>
            <h2> Tecnico Nombre</h2>
          </ion-label>
        </div>
        <div class="action-button">
          <ion-button>
            <ion-icon name="add"></ion-icon> Agregar Medicion 
          </ion-button>
        </div>
        <ion-list class="menu-items" lines="none">
          <ion-item class="active">
            <router-link to="/" style="text-decoration:none"><ion-icon name="home"></ion-icon> Home </router-link>
          </ion-item>
          <ion-item class="active">
            <router-link to="/usuarios" style="text-decoration:none"><ion-icon name="md-contacts"></ion-icon> Usuarios </router-link>
          </ion-item>
          <ion-item class="active">
            <router-link to="/rutas" style="text-decoration:none"><ion-icon name="git-branch"></ion-icon> Rutas </router-link>
          </ion-item>
          <ion-item class="active">
            <router-link to="/configuracion" style="text-decoration:none"><ion-icon name="settings"></ion-icon> Configuraciones </router-link>
          </ion-item>
        </ion-list>
      </ion-content>
    </ion-menu>
    <!-- <ion-content> -->
      <router-view id="main" />
    <!-- </ion-content> -->
  </ion-app>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
<script>
  export default {
     
  }
</script>