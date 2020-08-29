<template>
  <div>
    <HeaderComponent />
    <ion-header>
      <ion-toolbar>
          <ion-title>{{titulo}}</ion-title>
      </ion-toolbar>

      <ion-fab vertical="bottom" horizontal="start" edge slot="fixed" v-show="vista === 'usuarios'">
          <ion-fab-button @click="formAdd()">
              <ion-icon name="add"></ion-icon>
          </ion-fab-button>
      </ion-fab>
    </ion-header>
    
    <AddUserComponent 
      v-show="vista === 'edit' || vista === 'add'"
      :calles='calles' :usuarios='usuarios' :vista='vista' :datos='datos'
      @getDatos="getDatos" @pagNormal='pagNormal'
    />
    <ion-card v-show="vista === 'usuarios'">
      <ion-card-content>
        <ion-row>
          <ion-col size="8">
            <ion-searchbar placeholder="Busque Aqui" :value="filtro.toLowerCase()" @input= "filtro = $event.target.value"></ion-searchbar>
          </ion-col>
          <ion-col size="4">
            <ion-select :placeholder="opcion" :value="opcion" @ionChange="opcion= $event.target.value">
              <ion-select-option value= 'nombre' > Nombre</ion-select-option>
              <ion-select-option value= 'apellido' > Apellido</ion-select-option>
              <ion-select-option value= 'socio' > Socio</ion-select-option>
            </ion-select>
          </ion-col>
        </ion-row>
        <ion-grid>
          <ion-row >
            <ion-col size="3">
              <ion-label class="titulo-lista">Usuario</ion-label> 
            </ion-col>
            <ion-col size="3">
              <ion-label class="titulo-lista">Direccion</ion-label> 
            </ion-col>
            <ion-col size="2.5">
              <ion-label class="titulo-lista">Socio N°</ion-label> 
            </ion-col>
            <ion-col size="3">
              <ion-label class="titulo-lista">Opciones</ion-label> 
            </ion-col>
          </ion-row>
          <ion-row v-for="(usuario, index) of searchUsuarios" :key="index">
            <ion-col size="3">
              {{usuario.nombre}} {{usuario.apellido}}
            </ion-col>
            <ion-col size="3">
              {{usuario.direccion.calle}} {{usuario.direccion.numero}} 
            </ion-col>
            <ion-col size="2">
              {{usuario.socio}}
            </ion-col>
            <ion-col size="4">
                <ion-col size="1.7">
                  <ion-icon class="item-abm" name="eye" @click="cambiarVista(usuario, index)"></ion-icon>
                </ion-col>
                <ion-col >
                  <ion-icon class="item-abm" name="md-create" color="warning" @click="formEdit(usuario, index)"></ion-icon>
                </ion-col>
                <ion-col size="1.7">
                  <ion-icon class="item-abm" name="md-trash" color="danger" @click="eliminar(index)"></ion-icon>
                </ion-col>
            </ion-col>
          </ion-row>
        </ion-grid>
      </ion-card-content>
    </ion-card>
    <UserDetalle
      :datos='datos'
      @pagNormal='pagNormal'
      v-show="vista === 'user'"
    />
  </div>
</template>
<script>
  import HeaderComponent from '@/components/Header-Component.vue'
  import AddUserComponent from '@/components/AddUsuario-Component.vue'
  import UserDetalle from '@/components/UserDetalle-Component.vue'
  export default {
    name: 'Usuarios',
    components: {
      HeaderComponent,
      AddUserComponent,
      UserDetalle
    },
    data(){
      return{
        vista: "usuarios",
        titulo: "Lista Usuarios",
        datos: {
          user: {
            nombre: '',
            apellido: '',
            direccion: {
              calle: '',
              numero: '',
            },
            socio: '',
            clave: '',
            categoria: '',
          },
          index: ''
        },
        usuarios: [],
        calles: [],
        filtro: '',
        opcion: ''
      }
    },
    mounted(){
      this.getDatos();
    },
    computed:{       
      searchUsuarios: function () {
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
      getDatos(){
        let datosDB= JSON.parse(localStorage.getItem('usuarios'));
        if(datosDB != null){
          this.usuarios = datosDB;
        }
        datosDB= JSON.parse(localStorage.getItem('calles'));
        if(datosDB != null){
            this.calles = datosDB;
        }
      },
      pagNormal(){
        this.vista= 'usuarios';
        this.titulo= 'Lista de Usuarios'
      },
      agregar(){
        this.usuarios.push({
          nombre: this.user.nombre,
          apellido: this.user.apellido,
          direccion: this.user.direccion,
          categoria: this.user.categoria,
          clave: this.user.clave,
          socio: this.user.socio,
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
      formAdd(){
        this.titulo= 'Agregar Usuario'
        this.vista= 'add';
      },
      cambiarVista(user){
        this.titulo= 'Detalle de Usuario'
        this.datos.user= user;
        this.vista= 'user';
      },
      formEdit(user, index){
        this.titulo= 'Editar de Usuario'
        this.datos.user= user;
        this.datos.index= index;
        this.vista= 'edit';
      },
      eliminar(index){
        this.usuarios.splice(index, 1);
        localStorage.setItem('usuarios', JSON.stringify(this.usuarios));
      }
    }
  }
</script>