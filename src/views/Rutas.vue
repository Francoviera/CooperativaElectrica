<template>
    <div>
        <HeaderComponent />

        <!-- <ion-card>
          <ion-card-header>
            <ion-card-title>Agregar Ruta</ion-card-title>
          </ion-card-header> -->
        <ion-header>
            <ion-toolbar>
                <ion-title>{{titulo}}</ion-title>
            </ion-toolbar>
    
            <ion-fab vertical="bottom" horizontal="start" edge slot="fixed">
                <ion-fab-button>
                    <!-- <ion-icon name="settings"></ion-icon> -->
                    Rutas
                </ion-fab-button>
                <ion-fab-list side="end">
                    <ion-fab-button @click="pagAddRuta()"><ion-icon name="add"></ion-icon></ion-fab-button>
                    <ion-fab-button @click="pagRutas()"><ion-icon name="md-clipboard"></ion-icon></ion-fab-button>
                </ion-fab-list>
            </ion-fab>

            <ion-fab vertical="bottom" horizontal="end" edge slot="fixed">
                <ion-fab-button>
                    <!-- <ion-icon name="settings"></ion-icon> -->
                    Calles
                </ion-fab-button>
                <ion-fab-list side="start">
                    <ion-fab-button @click="pagAddCalle()"><ion-icon name="add"></ion-icon></ion-fab-button>
                    <ion-fab-button @click="pagCalles()"><ion-icon name="md-clipboard"></ion-icon></ion-fab-button>
                </ion-fab-list>
            </ion-fab>
        
        </ion-header>

        <!-- <ion-content> -->
            <AddRutasComponent v-show="ruta === 0"/>
            <RutasComponent v-show="ruta === 1"/>

            <AddCalleComponent 
              :calles='calles' :usuarios='usuarios' 
              @pagCalles="pagCalles"  @getDatos="getDatos" 
              v-show="calle === 0"
            />
            <CallesComponent 
              :calles='calles' :usuarios='usuarios'  
              @getDatos="getDatos" 
              v-show="calle === 1"
            />
        <!-- </ion-content>  -->
    </div>
</template>
<script>
  import HeaderComponent from '@/components/Header-Component.vue'
  import AddRutasComponent from '@/components/AddRutas-Component.vue'
  import RutasComponent from '@/components/Rutas-Component.vue'
  import AddCalleComponent from '@/components/AddCalle-Component.vue'
  import CallesComponent from '@/components/Calles-Component.vue'
  export default {
    name: 'Usuarios',
    components: {
      HeaderComponent,
      AddRutasComponent,
      RutasComponent,
      AddCalleComponent,
      CallesComponent
    },
    data(){
      return{
        titulo: "Opciones",
        ruta: '',
        calle: '',
        usuarios: [],
        calles: [], 
      }
    },
    mounted(){
      this.getDatos();
    },
    methods: {
      pagAddRuta(){
        this.calle= '';
        this.titulo= 'Agregar Ruta';
        this.ruta= 0;
      },
      pagRutas(){
        this.calle= '';
        this.titulo= 'Lista Rutas';
        this.ruta= 1;
      },
      pagAddCalle(){
        this.ruta= '';
        this.titulo= 'Agregar Calle';
        this.calle= 0;
      },
      pagCalles(){
        this.ruta= '';
        this.titulo= 'Lista de Calles';
        this.calle= 1;
      },
      getDatos(){
        let datosDB= JSON.parse(localStorage.getItem('calles'));
        if(datosDB != null){
            this.calles = datosDB;
        }
        datosDB= JSON.parse(localStorage.getItem('usuarios'));
        if(datosDB != null){
            this.usuarios = datosDB;
        }
      }
    }
  }
</script>