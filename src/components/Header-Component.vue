<template>
  <ion-header>
    <ion-toolbar color="dark">
      <ion-buttons slot="start">
        <ion-menu-button menu="first"><ion-icon slot="icon-only" name="menu" ></ion-icon></ion-menu-button>
      </ion-buttons>
      <ion-title>Cooperativa Electrica</ion-title>
    </ion-toolbar>
    
    <!-- <ion-router-outlet id="main"></ion-router-outlet> -->
  </ion-header>
</template>
<script>

  export default {

    methods: {
      openFirst() {
        this.menu.enable(true, 'first');
        this.menu.open('first');
      }
    }
  }
</script>