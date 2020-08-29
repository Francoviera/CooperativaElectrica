<template>
    <div>
        <HeaderComponent />

        <ion-card>
          <ion-card-header>
            <ion-card-title>Proximamente</ion-card-title>
            <ion-card-subtitle>Version Beta</ion-card-subtitle>
          </ion-card-header>
          <ion-card-content>
            <ion-title>Aqui prodra configurar: </ion-title>
            <ion-item>
              <ion-labe>*su cuenta con la base de datos y traer toda la informacion</ion-labe>
            </ion-item>
          </ion-card-content>
        </ion-card>
  </div>
</template>
<script>
  import HeaderComponent from '@/components/Header-Component.vue'
  export default {
    name: 'Configuraciones',
    components: {
      HeaderComponent
    },
  }
</script>