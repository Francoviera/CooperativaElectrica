<template>
    <ion-content>     
        ee
        
    </ion-content>
</template>
<script>
  export default {
    data(){
      return{
        rutas: [],
        ruta: {
            nombre: '',
            usuarios: [],
            calles: [],
        },
        usuarios: [],    

      }
    },
    mounted(){
        let datosDB= JSON.parse(localStorage.getItem('usuarios'));
        if(datosDB != null){
            this.usuarios = datosDB;
        }
        datosDB= JSON.parse(localStorage.getItem('rutas'));
        if(datosDB != null){
            this.rutas = datosDB;
        }
    },
    methods: {
      agregar(){
        this.rutas.push({
          nombre: this.nombre,
          apellido: this.apellido,
          direccion: this.direccion,
          categoria: this.categoria,
          clave: this.clave,
          socio: this.socio,
          estados: []
        });
        this.nombre= '';
        this.apellido= '';
        this.direccion= '';
        this.categoria= '';
        this.clave= '';
        this.socio= '';
        localStorage.setItem('usuarios', JSON.stringify(this.usuarios));
      },
      eliminar(index){
        this.usuarios.splice(index, 1);
        localStorage.setItem('usuarios', JSON.stringify(this.usuarios));
      }
    }
  }
</script>