<template>
  <ion-app id="app">
    <ion-toolbar color="dark">
      <ion-buttons >
        <ion-icon slot="icon-only" name="menu" @click="openFirst()"></ion-icon>
      </ion-buttons >
    </ion-toolbar>
    <ion-menu side="start" menu-id="first" content-id="main">
      <ion-header>
        <ion-toolbar color="dark">
          <ion-buttons >
            <ion-title>Menu</ion-title>
          </ion-buttons >
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <ion-list>
          <ion-item>Menu Item</ion-item>
          <ion-item>Menu Item</ion-item>
          <ion-item>Menu Item</ion-item>
          <ion-item>Menu Item</ion-item>
          <ion-item>Menu Item</ion-item>
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
  import { Component, Vue } from 'vue-property-decorator';

  @Component()
  export default class Example extends Vue {

    openFirst() {
      this.menu.enable(true, 'first');
      this.menu.open('first');
    }
  }
</script>