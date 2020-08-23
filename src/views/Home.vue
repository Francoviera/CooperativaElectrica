<template>
  <div>
    <HeaderComponent />
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
