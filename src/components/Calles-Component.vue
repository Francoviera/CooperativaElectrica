<template>
    <div>   
        <ion-card>  
            <ion-card-content v-show="vistaSimplificada === 0">
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
                            {{item}}
                        </ion-col>
                        <ion-col size="3.5">
                            {{cantUsuarios(item)}}
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
                            <ion-input class="form-control" :value="calle.nombre" @input= "calle.nombre = $event.target.value"></ion-input>
                        </ion-item>
                        <ion-card-content>
                            <ion-button type="submit" expand="block">Editar</ion-button>
                        </ion-card-content>
                    </form>
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
        vistaSimplificada: 0,
        calle:{
            nombre: '',
            usuarios: [],
            index: '',
        },
        direcciones: '',
        filtro: '',
      }
    },
    computed:{       
      searchUsuarios: function () {
        return this.calle.usuarios.filter((item) => item.toLowerCase().includes(this.filtro));
      },
      
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
        cantUsuarios: function(nombre){
            if(this.usuarios.length > 0){
                let users= 0;
                for (const i of this.usuarios) {
                    if( i.direccion.calle.toLowerCase() === nombre){
                        users++;
                    }
                }
                return users;
            }else{
                return 0;
            }
        },
        eliminar(index){
            this.calles.splice(index, 1);
            localStorage.setItem('calles', JSON.stringify(this.calles));
            this.$emit('getDatos');
        },
        cambiarVista(calle, index){
            this.vistaSimplificada= 1;
            this.calle.nombre= calle;
            if(this.usuarios.length > 0){
                for (let i = 0; i < this.usuarios.length; i++) {
                    const e = this.usuarios[i];
                     if( e.direccion.calle === calle){
                        this.usuarios.push({
                            nombre: e.nombre,
                            index: i
                        })
                    }
                }
                // this.calle.usuarios= users;
            } 
            this.calle.index= index;
        },
        invertirVista(){ 
            this.vistaSimplificada= 0;
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
        formEdit(calle, index){
            this.calle.nombre = calle;
            this.calle.index= index;
            this.vistaSimplificada= -1;
        },
        editarCalle(){
            this.calles[this.calle.index]= this.calle.nombre.toLowerCase();
            localStorage.setItem('calles', JSON.stringify(this.calles));
            this.vistaSimplificada= 0;
        }
    }
  }
</script>