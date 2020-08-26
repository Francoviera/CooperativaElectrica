<template>
  <div>
    <HeaderComponent />
    <ion-card>
      <ion-card-header>
      <ion-card-title>Home</ion-card-title>
      </ion-card-header>
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
