<template>
  <v-container>
    <v-row class="text-center" >
      <v-col class="mb-12">
  <v-card
    class="mx-auto "
  >
    <v-list-item>
      <v-list-item-content>
        <v-list-item-title class="headline">Gastos</v-list-item-title>
        <v-list-item-subtitle>Mi cuenta</v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

       <v-list >

         <v-list-item>
         
        <v-list-item-content>
          <v-list-item-title class='lista-header' >Descripcion</v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title class='lista-header' >fecha</v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title class='lista-header'  >monto</v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title class='lista-header' >motivo</v-list-item-title>
        </v-list-item-content>

          
      </v-list-item>

 <v-dialog v-model="dialogEdit" persistent max-width="600px">
   <template  v-slot:activator="{ on, attrs }">
      <v-list-item
        
        v-for="item in items"
        :key="item.mId"
       
        v-bind="attrs"
        v-on="on"
       
        
      >
       
        <v-list-item-content>
          <v-list-item-title v-text="item.descripcion"></v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title v-text="item.fecha"></v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title v-text="item.monto"></v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title v-text="item.motivo"></v-list-item-title>
        </v-list-item-content>
   
      </v-list-item>
      </template>
       <modal-movimiento class='md-2' :itemsPadre="items" @masMovimientos="actualizaItems" :accion='agregar' />
      </v-dialog>
    </v-list>
    <v-card-actions>

      <v-dialog v-model="dialog" persistent max-width="600px">
      <template  v-slot:activator="{ on, attrs }">
        <v-btn
          text
          color="deep-purple accent-4"
          v-bind="attrs"
          v-on="on"
          
        >
          agregar
        </v-btn>
      </template>
       <modal-movimiento class='md-2' :itemsPadre="items" @masMovimientos="actualizaItems" :accion='agregar' />
      </v-dialog>
  
      
      


      <v-dialog v-model="dialog2" persistent max-width="600px">
      <template  v-slot:activator="{ on, attrs }">
        <v-btn
          text
          color="deep-purple accent-4"
          v-bind="attrs"
          v-on="on"
          
        >
          editar
        </v-btn>
      </template>
      <modal-movimiento></modal-movimiento>
      </v-dialog>
   

    </v-card-actions>
  </v-card>

 <!-- modal --> 
  <!-- modal --> 
   <!-- modal --> 
    <!-- modal --> 







</v-col>
 

    </v-row>
  </v-container>
</template>

<script>
import ModalMovimiento from './ModalMovimiento.vue'
  export default {
    name: 'HelloWorld',
    components: {
      ModalMovimiento,
    },
    methods: {
      actualizaItems(movimientos){
        console.log('recibe')
        this.items = movimientos
         this.dialog=false
      },
      cierraDialogPadre(){
        console.log(this.dialog)
        this.dialog=false
      },
    
    },

    data: () => ({
        dialog: false,
        dialog2:false,
        dialogEdit:false,
        items: [
          { mId:'1', descripcion:"unas papas",fecha:"01-06-1990",monto:"500",motivo:"por que si"},
          { mId:'2', descripcion:"otras papas",fecha:"01-06-1990",monto:"600",motivo:"asdaf"},
          { mId:'3', descripcion:"uber",fecha:"01-06-1990",monto:"7000",motivo:"     "},
          { mId:'4', descripcion:"Mcdonals",fecha:"01-06-1990",monto:"8000",motivo:""},
          { mId:'5',descripcion:"chelas",fecha:"01-06-1990",monto:"13000",motivo:"sed"},
        ],
        editar: 'editar',
        agregar: 'agregar',
    
    }),
  }
</script>

<style scoped>
  .lista-header{
    font-weight: bolder;
    color:black;

  }
</style>