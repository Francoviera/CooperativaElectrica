<template>   
    <ion-card-content>     
        <form @submit.prevent="agregar">
            
            <ion-item>
                <ion-label position="floating">Nombre</ion-label>
                <ion-input class="form-control" :value="nombre" @input= "nombre = $event.target.value"></ion-input>
            </ion-item>
            <ion-item>
                <ion-select multiple="true" :value="direcciones" @ionChange="direcciones= $event.target.value">
                    <ion-select-option  v-for="(usuario, index) of usuarios" :key="index" :value="usuario.nombre">{{usuario.nombre}}</ion-select-option>
                </ion-select>
            </ion-item>
            <ion-card-content>
                <ion-button type="submit" expand="block">Agregar</ion-button>
            </ion-card-content>
        </form>
    </ion-card-content>
</template>
<script>
  export default {
    props:['calles', 'usuarios'],
    data(){
      return{
        direcciones: '',
        // calles: [],
        nombre: '',
        // usuarios: [],  
      }
    },
    // mounted(){
    //     let datosDB= JSON.parse(localStorage.getItem('calles'));
    //     if(datosDB != null){
    //         this.calles = datosDB;
    //     }
    //     datosDB= JSON.parse(localStorage.getItem('usuarios'));
    //     if(datosDB != null){
    //         this.usuarios = datosDB;
    //     }
    // },
    methods: {
      agregar(){
        let arreglo= this.direcciones.split(",");

        if(this.nombre != '' && this.direcciones != []){
            this.calles.push({
                nombre: this.nombre,
                usuarios: arreglo
            });
            localStorage.setItem('calles', JSON.stringify(this.calles));
            
            this.nombre= '';

            this.$emit('getDatos');
            this.$emit('pagCalles');
        }else{
            alert("Porfavor complete todos los Campos")
        }
      },
    }
  }
</script>