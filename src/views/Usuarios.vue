<template>
    <div>
        <HeaderComponent />

        <ion-card>
          <ion-card-header>
            <ion-card-title>Agregar Usuarios</ion-card-title>
          </ion-card-header>

          <ion-card-content>
            
            <form @submit.prevent="agregar">
              <ion-item>
                <ion-item>
                  <ion-label position="floating">Nombre</ion-label>
                  <ion-input class="form-control" :value="nombre" @input= "nombre = $event.target.value"></ion-input>
                </ion-item>
                <ion-item>
                  <ion-label position="floating">Apellido</ion-label>
                  <ion-input class="form-control" :value="apellido" @input= "apellido = $event.target.value"></ion-input>
                </ion-item>
              </ion-item>
              
              <ion-item>
                <ion-item>
                  <ion-label position="floating">Calle</ion-label>
                  <ion-select placeholder="Seleccione" :value="direccion.calle" @ionChange="direccion.calle= $event.target.value">
                    <ion-select-option v-for="(calle, index) of calles" :key="index" :value= calle> {{calle}}</ion-select-option>
                  </ion-select>
                </ion-item>
                <ion-item>
                  <ion-label position="floating">Numero</ion-label>
                  <ion-input class="form-control" :value="direccion.numero" @input= "direccion.numero = $event.target.value"></ion-input>
                </ion-item>
              </ion-item>
              <ion-item>
                <ion-item>
                  <ion-label position="floating">Socio N°</ion-label>
                  <ion-input class="form-control" :value="socio" @input= "socio = $event.target.value"></ion-input>
                </ion-item>
                <ion-item>
                  <ion-label position="floating">Cat N°</ion-label>
                  <ion-input class="form-control" :value="categoria" @input= "categoria = $event.target.value"></ion-input>
                </ion-item>
                <ion-item>
                  <ion-label position="floating">Clave N°</ion-label>
                  <ion-input class="form-control" :value="clave" @input= "clave = $event.target.value"></ion-input>
                </ion-item>
              </ion-item>
              <ion-card-content>
                <ion-button type="submit" expand="block">Agregar</ion-button>
            </ion-card-content>
            </form>
          </ion-card-content>
          

          <ion-card-header>
            <ion-card-title>Lista Usuarios</ion-card-title>

          </ion-card-header>
          <ion-card-content>
            <ion-grid>
              <ion-row >
                <ion-col size="4">
                  <ion-label>Usuario</ion-label> 
                </ion-col>
                <ion-col size="4">
                  Direccion 
                </ion-col>
                <ion-col size="4">
                  Socio N°
                </ion-col>
              </ion-row>
              <ion-row v-for="(usuario, index) of usuarios" :key="index">
                <ion-col>
                  {{usuario.nombre}} {{usuario.apellido}}
                </ion-col>
                <ion-col>
                  {{usuario.direccion.calle}} {{usuario.direccion.numero}} 
                </ion-col>
                <ion-col>
                  {{usuario.socio}}
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
    name: 'Usuarios',
    components: {
      HeaderComponent
    },
    data(){
      return{
          nombre: '',
          apellido: '',
          direccion: {
            calle: '',
            numero: ''
          },
          categoria: '',
          clave: '',
          socio: '',
          usuarios: [],
          calles: [],
      }
    },
    mounted(){
      let datosDB= JSON.parse(localStorage.getItem('usuarios'));
      if(datosDB != null){
        this.usuarios = datosDB;
      }
      datosDB= JSON.parse(localStorage.getItem('calles'));
      if(datosDB != null){
          this.calles = datosDB;
      }

    },
    methods: {
      agregar(){
        this.usuarios.push({
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
        this.direccion= {
          calle: '',
          numero: ''
        };
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