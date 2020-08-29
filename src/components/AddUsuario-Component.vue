<template>
    <ion-card>
        <ion-card-content v-show="vista === 'add'">
            <ion-buttons slot="primary">
              <ion-button size="small" color="medium" slot="start" @click="pagNormal()">
                <ion-icon name="ios-arrow-dropleft" ></ion-icon>
                <ion-label>  Atras</ion-label>
              </ion-button> 
            </ion-buttons>
            <form @submit.prevent="agregar">
                <ion-item>
                <ion-item>
                    <ion-label position="floating">Nombre</ion-label>
                    <ion-input class="form-control" :value="user.nombre" @input= "user.nombre = $event.target.value"></ion-input>
                </ion-item>
                <ion-item>
                    <ion-label position="floating">Apellido</ion-label>
                    <ion-input class="form-control" :value="user.apellido" @input= "user.apellido = $event.target.value"></ion-input>
                </ion-item>
                </ion-item>
                
                <ion-item>
                <ion-item>
                    <ion-label position="floating">Calle</ion-label>
                    <ion-select placeholder="Seleccione" :value="user.direccion.calle" @ionChange="user.direccion.calle= $event.target.value">
                    <ion-select-option v-for="(calle, index) of calles" :key="index" :value= calle> {{calle}}</ion-select-option>
                    </ion-select>
                </ion-item>
                <ion-item>
                    <ion-label position="floating">Numero</ion-label>
                    <ion-input class="form-control" :value="user.direccion.numero" @input= "user.direccion.numero = $event.target.value"></ion-input>
                </ion-item>
                </ion-item>
                <ion-item>
                <ion-item>
                    <ion-label position="floating">Socio N°</ion-label>
                    <ion-input class="form-control" :value="user.socio" @input= "user.socio = $event.target.value"></ion-input>
                </ion-item>
                <ion-item>
                    <ion-label position="floating">Cat N°</ion-label>
                    <ion-input class="form-control" :value="user.categoria" @input= "user.categoria = $event.target.value"></ion-input>
                </ion-item>
                <ion-item>
                    <ion-label position="floating">Clave N°</ion-label>
                    <ion-input class="form-control" :value="user.clave" @input= "clave = $user.event.target.value"></ion-input>
                </ion-item>
                </ion-item>
                <ion-card-content>
                <ion-button type="submit" expand="block">Agregar</ion-button>
            </ion-card-content>
        </form>
        </ion-card-content>

        <ion-card-content v-show="vista === 'edit'">  
            <ion-buttons slot="primary">
              <ion-button size="small" color="medium" slot="start" @click="pagNormal()">
                <ion-icon name="ios-arrow-dropleft" ></ion-icon>
                <ion-label>  Atras</ion-label>
              </ion-button> 
            </ion-buttons>       
            <form @submit.prevent="editar">
                <ion-item>
                    <ion-item>
                    <ion-label position="floating">Nombre</ion-label>
                    <ion-input class="form-control" :value="datos.user.nombre" @input= "user.nombre = $event.target.value"></ion-input>
                    </ion-item>
                    <ion-item>
                    <ion-label position="floating">Apellido</ion-label>
                    <ion-input class="form-control" :value="datos.user.apellido" @input= "user.apellido = $event.target.value"></ion-input>
                    </ion-item>
                </ion-item>
                
                <ion-item>
                    <ion-item>
                    <ion-label position="floating">Calle</ion-label>
                    <ion-select placeholder="Seleccione" :value="datos.user.direccion.calle" @ionChange="user.direccion.calle= $event.target.value">
                        <ion-select-option v-for="(calle, index) of calles" :key="index" :value= calle> {{calle}}</ion-select-option>
                    </ion-select>
                    </ion-item>
                    <ion-item>
                    <ion-label position="floating">Numero</ion-label>
                    <ion-input class="form-control" :value="datos.user.direccion.numero" @input= "user.direccion.numero = $event.target.value"></ion-input>
                    </ion-item>
                </ion-item>
                <ion-item>
                    <ion-item>
                    <ion-label position="floating">Socio N°</ion-label>
                    <ion-input class="form-control" :value="datos.user.socio" @input= "user.socio = $event.target.value"></ion-input>
                    </ion-item>
                    <ion-item>
                    <ion-label position="floating">Cat N°</ion-label>
                    <ion-input class="form-control" :value="datos.user.categoria" @input= "user.categoria = $event.target.value"></ion-input>
                    </ion-item>
                    <ion-item>
                    <ion-label position="floating">Clave N°</ion-label>
                    <ion-input class="form-control" :value="datos.user.clave" @input= "user.clave = $event.target.value"></ion-input>
                    </ion-item>
                </ion-item>
                <ion-card-content>
                    <ion-button type="submit" color="warning">Editar</ion-button>
                    <ion-button color="medium" @click="pagNormal()">Cancelar</ion-button>
                </ion-card-content>
            </form>
        </ion-card-content>
    </ion-card>
</template>
<script>
  export default {
    props:['calles', 'usuarios', 'vista', 'datos'],
    data(){
      return{
        user:{  
          nombre: '',
          apellido: '',
          direccion: {
              calle: '',
              numero: '',
          },
          categoria: '',
          clave: '',
          socio: '',
        },
      }
    },
    computed:{       
      searchUsuarios: function () {
        return this.usuarios.filter((item) => item.nombre.includes(this.filtro));
      }
    },
    methods: {
      pagNormal(){
        this.$emit('pagNormal');
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
        this.$emit('getDatos');
        this.$emit('pagNormal');
      },
      editar(){
        this.usuarios[this.datos.index]= this.user;
        localStorage.setItem('usuarios', JSON.stringify(this.usuarios));
        this.user.nombre= '';
        this.user.apellido= '';
        this.user.direccion= {
          calle: '',
          nombre: '',
        };
        this.user.categoria= '';
        this.user.clave= '';
        this.user.socio= '';

        this.$emit('getDatos');
        this.$emit('pagNormal');
      },
    }
  }
</script>