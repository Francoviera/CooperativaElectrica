<template>
    <div>
        <HeaderComponent />

        <ion-card v-show="!agregandoMedicion">
            <ion-card-header>
            <ion-card-subtitle>Lista de Usuarios</ion-card-subtitle>
            </ion-card-header>

            <ion-card-content>
                <ion-item>
                  <ion-item>
                    <ion-label position="floating">Filtro</ion-label>
                    <ion-input class="form-control" :value="filtro.toLowerCase()" @input= "filtro = $event.target.value"></ion-input>
                  </ion-item>

                    <ion-select placeholder="Seleccione" :value="opcion" @ionChange="opcion= $event.target.value">
                        <ion-select-option value= 'nombre' > Nombre</ion-select-option>
                        <ion-select-option value= 'apellido' > Apellido</ion-select-option>
                        <ion-select-option value= 'socio' > Socio</ion-select-option>
                    </ion-select>

                </ion-item>
                
            </ion-card-content> 
            <ion-card-content>
                 <ion-grid>
              <ion-row >
                <ion-col size="3">
                  <ion-label class="titulo-lista">Usuario</ion-label> 
                </ion-col>
                <ion-col size="3">
                  <ion-label class="titulo-lista">Direccion </ion-label> 
                </ion-col>
                <ion-col size="3">
                  <ion-label class="titulo-lista">Socio N°</ion-label>                  
                </ion-col>
                <ion-col size="3">
                  <ion-label class="titulo-lista">Opcion</ion-label>                   
                </ion-col>
              </ion-row>
              <ion-row v-for="(usuario, index) of searchProducts" :key="index">
                <ion-col>
                  {{usuario.nombre}} {{usuario.apellido}}
                </ion-col>
                <ion-col>
                  {{usuario.direccion.calle}} {{usuario.direccion.numero}} 
                </ion-col>
                <ion-col>
                  {{usuario.socio}}
                </ion-col>
                <ion-col>
                  <ion-button size="small" color="light" @click="cambiarVista(usuario, index)"><ion-icon name="ios-create"></ion-icon></ion-button>
                </ion-col>
              </ion-row>
            </ion-grid>     
            </ion-card-content> 
        </ion-card>

        <ion-card v-show="agregandoMedicion">
            <ion-card-content v-show="!formEdit">
              <ion-buttons slot="primary">
                <ion-button size="small" color="medium" slot="start" @click="invertirVista()">
                    <ion-icon name="ios-arrow-dropleft" ></ion-icon>
                    <ion-label>  Atras</ion-label>
                </ion-button> 
              </ion-buttons>
              <form @submit.prevent="agregarMedicion">
                <ion-item>
                  <ion-item>
                    <ion-label position="floating"> Kwh Lectura</ion-label>
                    <ion-input class="form-control" :value="medicion.kwh.lectura" @input= "medicion.kwh.lectura = $event.target.value"></ion-input>
                  </ion-item>

                  <ion-item>
                    <ion-label position="floating"> Kwh Consumo</ion-label>
                    <ion-input class="form-control" :value="medicion.kwh.consumo" @input= "medicion.kwh.consumo = $event.target.value"></ion-input>
                  </ion-item>
                </ion-item>
                
                <ion-item>
                  <ion-item>
                    <ion-label position="floating"> Agua Lectura</ion-label>
                    <ion-input class="form-control" :value="medicion.agua.lectura" @input= "medicion.agua.lectura = $event.target.value"></ion-input>
                  </ion-item>

                  <ion-item>
                    <ion-label position="floating"> Agua Consumo</ion-label>
                    <ion-input class="form-control" :value="medicion.agua.consumo" @input= "medicion.agua.consumo = $event.target.value"></ion-input>
                  </ion-item>
                </ion-item>

                  <ion-card-content>
                    <ion-button type="submit" expand="block" color="success">Agregar</ion-button>
                </ion-card-content>
              </form>   
          </ion-card-content> 

          <ion-card-content v-show="formEdit">
              <ion-buttons slot="primary">
                <ion-button size="small" color="medium" slot="start" @click="invertirVista()">
                    <ion-icon name="ios-arrow-dropleft" ></ion-icon>
                    <ion-label>  Atras</ion-label>
                </ion-button> 
              </ion-buttons>
              <form @submit.prevent="editarMedicion">
                <ion-item>
                  <ion-item>
                    <ion-label position="floating"> Kwh Lectura</ion-label>
                    <ion-input class="form-control" :value="medicion.kwh.lectura" @input= "medicion.kwh.lectura = $event.target.value"></ion-input>
                  </ion-item>

                  <ion-item>
                    <ion-label position="floating"> Kwh Consumo</ion-label>
                    <ion-input class="form-control" :value="medicion.kwh.consumo" @input= "medicion.kwh.consumo = $event.target.value"></ion-input>
                  </ion-item>
                </ion-item>
                
                <ion-item>
                  <ion-item>
                    <ion-label position="floating"> Agua Lectura</ion-label>
                    <ion-input class="form-control" :value="medicion.agua.lectura" @input= "medicion.agua.lectura = $event.target.value"></ion-input>
                  </ion-item>

                  <ion-item>
                    <ion-label position="floating"> Agua Consumo</ion-label>
                    <ion-input class="form-control" :value="medicion.agua.consumo" @input= "medicion.agua.consumo = $event.target.value"></ion-input>
                  </ion-item>
                </ion-item>

                <ion-card-content>
                  <ion-button slot="start" type="submit" color="warning">Editar </ion-button>
                  <ion-button slot="end" color="medium" @click="invertirVistaEdit()">Cancelar</ion-button>
                </ion-card-content>
              </form>   
          </ion-card-content>

          <ion-card-header>
            <ion-card-title>Mediciones</ion-card-title>
          </ion-card-header>
          <ion-card-content>
            <ion-grid>
              <ion-row >
                 <ion-col size="2">
                  <ion-label class="titulo-lista">Mes</ion-label> 
                </ion-col>
                <ion-col size="4">
                  <ion-label class="titulo-lista">Kwh</ion-label> 
                </ion-col>
                <ion-col size="6">
                  <ion-label class="titulo-lista">Agua</ion-label> 
                </ion-col>
              </ion-row>
              <ion-row >
                 <ion-col size="2">
                </ion-col>
                <ion-col size="2.5">
                  <ion-label class="subtitulo-lista">Lectura</ion-label>   
                </ion-col>
                <ion-col size="2.5">
                  <ion-label class="subtitulo-lista">Consumo</ion-label>    
                </ion-col>
                <ion-col size="2.5">
                  <ion-label class="subtitulo-lista">Lectura</ion-label>   
                </ion-col>
                <ion-col size="2.5">
                  <ion-label class="subtitulo-lista">Consumo</ion-label>    
                </ion-col>
              </ion-row>
              <ion-row v-for="(medicion, index) of usuario.estados" :key="index">
                <ion-col size="2" @click="cambiarVistaEdit(medicion, index)">
                  {{medicion.mes}}
                </ion-col>
                <ion-col size="2.5">
                  {{medicion.kwh.lectura}} 
                </ion-col>
                <ion-col size="2.5">
                  {{medicion.kwh.consumo}} 
                </ion-col>
                <ion-col size="2.5">
                  {{medicion.agua.lectura}} 
                </ion-col>
                <ion-col size="2.5">
                  {{medicion.agua.consumo}} 
                </ion-col>
              </ion-row>
            </ion-grid>
          </ion-card-content>
        </ion-card>
    </div>
</template>
<script>
  import HeaderComponent from '@/components/Header-Component.vue'
  export default {
    name: 'AgregarMedicion',
    components: {
      HeaderComponent
    },
    data(){
      return{
        agregandoMedicion: false,
        formEdit: false,
        opcion: '',
        filtro: '',
        año: '',
        mes: '',
        fecha: '',
        usuario: '',
        indexEdit: '',
        medicion: {
          kwh:{
            lectura: '',
            consumo: ''
          },
          agua:{
            lectura: '',
            consumo: ''
          },
          },
        index: '',
        usuarios: [],
      }
    },
    mounted(){
      let datosDB= JSON.parse(localStorage.getItem('usuarios'));
      if(datosDB === null){
        this.usuarios = [];
      }else{
        this.usuarios = datosDB;
      }
      var fecha = new Date();
      this.año = fecha.getFullYear();
      this.mes = fecha.getMonth();

    },
    computed:{       
      searchProducts: function () {
        if(this.opcion === 'nombre'){
          return this.usuarios.filter((item) => item.nombre.includes(this.filtro));
        }
        if(this.opcion === 'apellido'){
          return this.usuarios.filter((item) => item.apellido.includes(this.filtro));
        }
        if(this.opcion === 'socio'){
          return this.usuarios.filter((item) => item.socio.includes(this.filtro));
        }
        return this.usuarios.filter((item) => item.nombre.toLowerCase().includes(this.filtro));
      }
    },
    methods: {
      cambiarVista(usuario, index){
        this.agregandoMedicion= true;
        this.usuario= usuario;
        this.index= index;
      },
      invertirVista(){
        this.medicion.kwh={
          lectura: '',
          consumo: ''
        }
        this.medicion.agua={
          lectura: '',
          consumo: ''
        },
        this.agregandoMedicion= false;
      },
      agregarMedicion(){
        if(this.medicion.kwh.lectura != '' && this.medicion.kwh.consumo != '' && this.medicion.agua.lectura != '' && this.medicion.agua.consumo != ''){
          this.usuarios[this.index].estados.push({
            año: this.año,
            mes: this.mes,
            kwh:{
              lectura: this.medicion.kwh.lectura,
              consumo: this.medicion.kwh.consumo
            },
            agua:{
              lectura: this.medicion.agua.lectura,
              consumo: this.medicion.agua.consumo
            },
          });
          this.medicion= {
            kwh:{
              lectura: '',
              consumo: ''
            },
            agua:{
              lectura: '',
              consumo: ''
            },
          },

          localStorage.setItem('usuarios', JSON.stringify(this.usuarios));
        }else{
          alert("Porfavor complete todos los campos");
        }
      },
      cambiarVistaEdit(medicion, index){
        this.formEdit= true;
        this.medicion= medicion;
        this.indexEdit= index;
      },
      invertirVistaEdit(){
        this.formEdit= false;
        this.medicion= {
          kwh:{
            lectura: '',
            consumo: ''
          },
          agua:{
            lectura: '',
            consumo: ''
          },
        },
        this.indexEdit= '';
      },
      editarMedicion(){
        if(this.medicion.kwh.lectura != '' && this.medicion.kwh.consumo != '' && this.medicion.agua.lectura != '' && this.medicion.agua.consumo != ''){
          console.log(this.usuarios[this.index].estados[this.indexEdit]);
          this.usuarios[this.index].estados[this.indexEdit]= {
            año: this.año,
            mes: this.mes,
            kwh:{
              lectura: this.medicion.kwh.lectura,
              consumo: this.medicion.kwh.consumo
            },
            agua:{
              lectura: this.medicion.agua.lectura,
              consumo: this.medicion.agua.consumo
            },
          }

          this.medicion= {
            kwh:{
              lectura: '',
              consumo: ''
            },
            agua:{
              lectura: '',
              consumo: ''
            },
          }         
          localStorage.setItem('usuarios', JSON.stringify(this.usuarios));    
          
          this.invertirVistaEdit();
        }else{
          alert("Porfavor complete todos los campos");
        }
      },
    }
  }
</script>