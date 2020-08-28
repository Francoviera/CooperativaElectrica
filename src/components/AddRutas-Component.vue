<template>   
    <ion-card-content>     
        <form @submit.prevent="agregar">
            
            <ion-item>
                <ion-label position="floating">Nombre</ion-label>
                <ion-input class="form-control" :value="ruta.nombre" @input= "ruta.nombre = $event.target.value"></ion-input>
            </ion-item>
            <ion-item>
              <ion-label position="floating">Seleccione</ion-label>
                <ion-select :placeholder="ruta.calles" multiple="true" :value="ruta.calles" @ionChange="ruta.calles= $event.target.value">
                    <ion-select-option  v-for="(calle, index) of calles" :key="index" :value="calle">{{calle}}</ion-select-option>
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
    props:['rutas','calles', 'usuarios'],
    data(){
      return{
        ruta: {
          nombre: '',
          calles: [],
        },
      }
    },
    mounted(){
      console.log(this.ruta.calles);
    },
    methods: {
      agregar(){
        let arreglo= this.ruta.calles.split(",");

        if(this.ruta.nombre != ''){
            this.rutas.push({
                nombre: this.ruta.nombre,
                calles: arreglo
            });
            localStorage.setItem('rutas', JSON.stringify(this.rutas));
            
            this.ruta.nombre= '';
            this.ruta.calles= [];

            this.$emit('getDatos');
            this.$emit('pagRutas');
        }else{
            alert("Porfavor complete todos los Campos")
        }

      },
    }
  }
</script>