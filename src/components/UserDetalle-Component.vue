<template>
    <ion-card>  
        <ion-card-content>
            <ion-buttons slot="primary">
                <ion-button size="small" color="medium" slot="start" @click="pagNormal()">
                    <ion-icon name="ios-arrow-dropleft" ></ion-icon>
                    <ion-label>  Atras</ion-label>
                </ion-button> 
            </ion-buttons>
            <ion-grid>
                <ion-list>
                    <ion-item>
                        <ion-col size="6">
                            <ion-label class="titulo-lista">Nombre:</ion-label> 
                        </ion-col>
                        <ion-col size="6">
                            <ion-label>{{datos.user.nombre}}</ion-label> 
                        </ion-col>               
                    </ion-item>
                    <ion-item>
                        <ion-col size="6">
                            <ion-label class="titulo-lista">Apellido:</ion-label> 
                        </ion-col>
                        <ion-col size="6">
                            <ion-label>{{datos.user.apellido}}</ion-label> 
                        </ion-col>
                    </ion-item>
                    <ion-item>
                        <ion-col size="6">
                            <ion-label class="titulo-lista">Direccion:</ion-label> 
                        </ion-col>
                        <ion-col size="6">
                            <ion-label>{{datos.user.direccion.calle}} {{datos.user.direccion.numero}}</ion-label> 
                        </ion-col>
                    </ion-item>
                    <ion-item>
                        <ion-col size="6">
                            <ion-label class="titulo-lista">N° Socio:</ion-label> 
                        </ion-col>
                        <ion-col size="6">
                            <ion-label>{{datos.user.socio}}</ion-label> 
                        </ion-col>
                    </ion-item>
                    <ion-item>
                        <ion-col size="6">
                            <ion-label class="titulo-lista">Clave:</ion-label> 
                        </ion-col>
                        <ion-col size="6">
                            <ion-label>{{datos.user.clave}}</ion-label> 
                        </ion-col>
                    </ion-item>
                    <ion-item>
                        <ion-col size="6">
                            <ion-label class="titulo-lista">Categoria:</ion-label> 
                        </ion-col>
                        <ion-col size="6">
                            <ion-label>{{datos.user.categoria}}</ion-label> 
                        </ion-col>
                    </ion-item>
                </ion-list>
            </ion-grid>
        </ion-card-content>
    </ion-card>
</template>
<script>

  export default {
    props:['datos'],
    methods: {
      pagNormal(){
        this.$emit('pagNormal');
      }
    }
  }
</script>