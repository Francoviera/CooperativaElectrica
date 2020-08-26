<template>
    <ion-card-content>     
        <form @submit.prevent="agregar">
            <ion-item>
                <ion-item>
                    <ion-label position="floating">Nombre</ion-label>
                    <ion-input class="form-control" :value="ruta.nombre" @input= "ruta.nombre = $event.target.value"></ion-input>
                </ion-item>
            </ion-item>
            <ion-card-content>
            <ion-button type="submit" expand="block">Agregar</ion-button>
        </ion-card-content>
        </form>
    </ion-card-content>
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
        let datosDB= JSON.parse(localStorage.getItem('rutas'));
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