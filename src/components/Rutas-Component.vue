<template>
    <div>   
        <ion-card>  
            <ion-card-content v-show="vistaSimplificada === 0">
                <!-- <ion-searchbar placeholder="Busque Aqui" :value="filtro.toLowerCase()" @input= "filtro = $event.target.value"></ion-searchbar> -->
                <ion-grid>
                    <ion-row >
                        <ion-col size="4">
                            <ion-label class="titulo-lista">Rutas </ion-label> 
                        </ion-col>
                        <ion-col size="3.7">
                            <ion-label class="titulo-lista">Cant Calles</ion-label> 
                        </ion-col>
                        <ion-col size="4">
                            <ion-label class="titulo-lista">Opciones </ion-label> 
                        </ion-col>
                    </ion-row>
                    <ion-row v-for="(item, index) of rutas" :key="index">
                        <ion-col size="4">
                            {{item.nombre}}
                        </ion-col>
                        <ion-col size="3.5">
                            {{item.calles.length}}
                        </ion-col>
                        <ion-col size="1.5">
                            <ion-icon class="item-abm" name="eye" @click="cambiarVista(item, index)"></ion-icon>
                        </ion-col>
                        <ion-col size="1.5">
                            <ion-icon class="item-abm" name="md-create" color="warning" @click="formEdit(item, index)"></ion-icon>
                        </ion-col>
                        <ion-col size="1.5">
                            <ion-icon class="item-abm" name="md-trash" color="danger" @click="eliminar(index)"></ion-icon>
                        </ion-col>
                    </ion-row>
                </ion-grid>
            </ion-card-content>
            <ion-card-content v-show="vistaSimplificada === 1">
                <ion-buttons slot="primary">
                    <ion-button size="small" color="medium" slot="start" @click="invertirVista()">
                        <ion-icon name="ios-arrow-dropleft" ></ion-icon>
                        <ion-label>  Atras</ion-label>
                    </ion-button> 
                </ion-buttons>
                <ion-list>
                    <ion-searchbar placeholder="Busque Aqui" :value="filtro.toLowerCase()" @input= "filtro = $event.target.value"></ion-searchbar>
                    <ion-item-sliding v-for="(calle, index) of searchCalles" :key="index">
                        <ion-item>
                            <ion-icon name="md-person"> </ion-icon>
                            <ion-label>{{calle}}</ion-label>
                        </ion-item>
                        <ion-item-options side="end">
                            <ion-item-option color="primary" @click="verUsuario(index)">Ver Calle</ion-item-option>
                        </ion-item-options>
                    </ion-item-sliding>
                </ion-list>
            </ion-card-content>
            <ion-card-content v-show="vistaSimplificada === -1">
                <ion-buttons slot="primary">
                    <ion-button size="small" color="medium" slot="start" @click="invertirVista()">
                        <ion-icon name="ios-arrow-dropleft" ></ion-icon>
                        <ion-label> Atras</ion-label>
                    </ion-button> 
                </ion-buttons>
                <ion-list>
                    <form @submit.prevent="editarCalle">
                        <ion-item>
                            <ion-label position="floating">Nombre</ion-label>
                            <ion-input class="form-control" :value="ruta.nombre.toLowerCase()" @input= "ruta.nombre = $event.target.value"></ion-input>
                        </ion-item>
                        <ion-item>
                            <ion-label v-if="(ruta.callesEdit != [])" position="floating">Seleccione</ion-label>
                            <ion-label v-else >Seleccione</ion-label>
                            <ion-select :placeholder="ruta.callesEdit" multiple="true" :value="ruta.calles" @ionChange="ruta.callesEdit= $event.target.value">
                                <div v-for="(calle, index) of calles" :key="index">
                                    <ion-select-option v-if=" ruta.callesEdit.includes(calle)" selected= true :value="calle">{{calle}}</ion-select-option>

                                    <ion-select-option v-else :value="calle">{{calle}}</ion-select-option>
                                </div>
                            </ion-select>
                        </ion-item>
                        <ion-card-content>
                            <ion-button slot="start" type="submit" color="warning">Editar </ion-button>
                        </ion-card-content>
                    </form>
                </ion-list>
            </ion-card-content>
        </ion-card>     
    </div>
</template>
<script>
  export default {
    props:['rutas','calles', 'usuarios'],
    data(){
      return{
        vistaSimplificada: 0,
        ruta:{
            nombre: '',
            calles: [],
            callesEdit: [],
            index: '',
        },
        direcciones: '',
        filtro: '',
      }
    },
    computed:{       
      searchCalles: function () {
        if(this.vistaSimplificada === 1){
            return this.ruta.calles.filter((item) => item.includes(this.filtro)); 
        }else{
            return '';        }
      },
      
    },
    methods: {
        cantCalles: function(nombre){
            if(this.calles.length > 0){
                let calles= 0;
                for (const i of this.calles) {
                    if( i === nombre){
                        calles++;
                    }
                }
                return calles;
            }else{
                return 0;
            }
        },
        eliminar(index){
            this.rutas.splice(index, 1);
            localStorage.setItem('rutas', JSON.stringify(this.rutas));
            this.$emit('getDatos');
        },
        cambiarVista(ruta, index){
            this.vistaSimplificada= 1;
            this.ruta.nombre= ruta.nombre;
            for (const ruta of ruta.calles) {
                this.ruta.calles.push(ruta);
            }
            this.ruta.index= index;
        },
        invertirVista(){ 
            this.ruta= {
                nombre: '',
                calles: [],
                callesEdit: [],
                index: ''
            }

            // this.ruta.nombre= '';
            // this.ruta.calles= new Array(2);
            // this.ruta.index= '';
            this.vistaSimplificada= 0;
        },
        // eliminarUsuario(index){
        //     this.calle.usuarios.splice(index, 1);
        //     this.calles[this.calle.index]= this.calle;
        //     localStorage.setItem('calles', JSON.stringify(this.calles));
        //     this.$emit('getDatos');
        // },
        verUsuario(index){
            console.log(this.calles[index]); //mostrar una alerta con los detalles del usuario o redirigirlo a otra vista
        },
        formEdit(ruta, index){
            this.ruta.nombre = ruta.nombre;
            this.ruta.callesEdit= ruta.calles;
            this.ruta.index= index;
            this.vistaSimplificada= -1;
        },
        editarCalle(){
            let arreglo= this.ruta.callesEdit.split(",");
            this.rutas[this.ruta.index]= {
                nombre: this.ruta.nombre,
                calles: arreglo
            };
            localStorage.setItem('rutas', JSON.stringify(this.rutas));
            this.$emit('getDatos');
            this.vistaSimplificada= 0;
        }
    }
  }
</script>