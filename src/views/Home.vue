<template>
  <div>
    <HeaderComponent />
    <ion-card>
      <ion-card-header>
        <ion-card-title>Home</ion-card-title>
        <ion-card-subtitle>¡¡Este es un prototipo!!</ion-card-subtitle>
      </ion-card-header>
      <ion-card-content>
        <div>
          <ion-title>Proximamente podra:</ion-title>
          <ion-item>
            <ion-label>*iniciar session con su cuenta</ion-label>
          </ion-item>
          <ion-item>
            <ion-label>*ver sus tareas y recorridos pendientes</ion-label>
          </ion-item>
        </div>
      </ion-card-content>
    </ion-card>
    <!-- <Usuarios-Component  
      v-show="url == 'usuarios'"> 
    </Usuarios-Component> -->
  </div>
</template>

<script>
  import HeaderComponent from '@/components/Header-Component.vue'
  export default {
    name: 'Home',
    components: {
      HeaderComponent
    },
    data: function(){
      return{
          url: "home",
      }
    },
    methods: {
      pagUsuarios(){
        this.getUsuarios();
        this.url= 'usuarios';
      },
    }
  }
</script>
