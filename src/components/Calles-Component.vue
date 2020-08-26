<template>
    <div>   
        <ion-card>  
            <ion-card-content v-show="!vistaSimplificada">
                <!-- <ion-searchbar placeholder="Busque Aqui" :value="filtro.toLowerCase()" @input= "filtro = $event.target.value"></ion-searchbar> -->
                <ion-grid>
                    <ion-row >
                        <ion-col size="4">
                            <ion-label class="titulo-lista">Calles </ion-label> 
                        </ion-col>
                        <ion-col size="3.7">
                            <ion-label class="titulo-lista">Cant Usuarios</ion-label> 
                        </ion-col>
                        <ion-col size="4">
                            <ion-label class="titulo-lista">Opciones </ion-label> 
                        </ion-col>
                    </ion-row>
                    <ion-row v-for="(item, index) of calles" :key="index">
                        <ion-col size="4">
                            {{item.nombre}}
                        </ion-col>
                        <ion-col size="3.5">
                            {{item.usuarios.length}}
                        </ion-col>
                        <ion-col size="1.5">
                            <ion-icon class="item-abm" name="eye" @click="cambiarVista(item, index)"></ion-icon>
                        </ion-col>
                        <ion-col size="1.5">
                            <ion-icon class="item-abm" name="md-create" color="warning"></ion-icon>
                        </ion-col>
                        <ion-col size="1.5">
                            <ion-icon class="item-abm" name="md-trash" color="danger" @click="eliminar(index)"></ion-icon>
                        </ion-col>
                    </ion-row>
                </ion-grid>
            </ion-card-content>
            <ion-card-content v-show="vistaSimplificada">
                <ion-buttons slot="primary">
                    <ion-button size="small" color="medium" slot="start" @click="invertirVista()">
                        <ion-icon name="ios-arrow-dropleft" ></ion-icon>
                        <ion-label>  Atras</ion-label>
                    </ion-button> 
                </ion-buttons>
                <ion-list>
                    <ion-searchbar placeholder="Busque Aqui" :value="filtro.toLowerCase()" @input= "filtro = $event.target.value"></ion-searchbar>
                    <ion-item-sliding v-for="(user, index) of searchUsuarios" :key="index">
                        <ion-item>
                            <ion-icon name="md-person"> </ion-icon>
                            <ion-label>{{user}}</ion-label>
                        </ion-item>
                        <ion-item-options side="end">
                            <ion-item-option color="danger" @click="eliminarUsuario(index)">Eliminar</ion-item-option>
                        </ion-item-options>
                    </ion-item-sliding>
                </ion-list>
            </ion-card-content>
        </ion-card>     
    </div>
</template>
<script>
  export default {
    props:['calles', 'usuarios'],
    data(){
      return{
        vistaSimplificada: false,
        // calles: [],
        calle:{
            nombre: '',
            usuarios: [],
            index: '',
        },
        // usuarios: [],  
        filtro: '',
      }
    },
    computed:{       
      searchUsuarios: function () {
        return this.calle.usuarios.filter((item) => item.toLowerCase().includes(this.filtro));
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
        eliminar(index){
            this.calles.splice(index, 1);
            localStorage.setItem('calles', JSON.stringify(this.calles));
            this.$emit('getDatos');
        },
        cambiarVista(calle, index){
            this.vistaSimplificada= true;
            this.calle.nombre= calle.nombre;
            this.calle.usuarios= calle.usuarios;
            this.calle.index= index;
        },
        invertirVista(){ 
            this.vistaSimplificada= false;
            this.calle.nombre= '';
            this.calle.usuarios= [];
            this.calle.index= '';
        },
        eliminarUsuario(index){
            this.calle.usuarios.splice(index, 1);
            this.calles[this.calle.index]= this.calle;
            localStorage.setItem('calles', JSON.stringify(this.calles));
            this.$emit('getDatos');
        },
    }
  }
</script>