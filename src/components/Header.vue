<template>
<v-dialog v-model="dialog" persistent max-width="600px">
      <template v-if="accion==='agregar'"  v-slot:activator="{ on, attrs }">
        <v-btn
          text
          color="deep-purple accent-4"
          v-bind="attrs"
          v-on="on"
          
        >
          agregar
        </v-btn>
      </template>
   
      <v-card>
        <v-card-title>
          <span class="headline">Nuevo Movimiento</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field label="motivo" required
                 v-model="motivo"></v-text-field>
              </v-col>
              <v-col cols="12" >
                <v-text-field label="fecha"
                 v-model="fecha" required></v-text-field>
              </v-col>
              <v-col cols="12" >
                <v-text-field label="monto" 
                 v-model="monto"
                 required></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field label="descripcion" 
                 v-model="descripcion"
                required></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="agregaMovimiento">Agregar</v-btn>
          <v-btn color="blue darken-1" text @click="dialog = false">Salir</v-btn>
        </v-card-actions>
      </v-card>
   
</template>

<script>
  export default {

    name: 'ModalMovimiento',
    props: ['itemsPadre'],

    data: () => ({
       motivo: '',
       fecha: '',
       descripcion: '',
       monto:'', 
       dialog: false,
       movimientos: [],
   
    }),
    methods: {
        agregaMovimiento(event){
            console.log('Entra')
            
            let movimiento = {
                motivo: this.motivo,
                fecha: this.fecha,
                descripcion: this.descripcion,
                monto: this.monto,
                mId:'',
            }
            
            let mId = 0
            this.itemsPadre.forEach(element => {
                let objeto = {
                mid:element.mid,
                motivo: element.motivo,
                fecha: element.fecha,
                descripcion: element.descripcion,
                monto: element.monto,
                }
                this.movimientos.push(objeto)
                mId++
            });
            
            movimiento.mId = mId
          
            this.movimientos.unshift(movimiento)
            this.dialog = false
            console.log('emite')
            this.$emit('masMovimientos',this.movimientos)
            this.movimientos=[]
            
           
            
        }
    }
  }
</script>

