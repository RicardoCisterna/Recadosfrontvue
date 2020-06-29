<template>
  <v-container>
    <v-row class="text-center" >
      <v-col class="mb-12">
  <v-card
    class="mx-auto "
    elevation='6'
  >
       <v-toolbar
      color="primary"
      
      dark
    >
     

      <v-toolbar-title >Recados</v-toolbar-title>

      <v-spacer></v-spacer>

    </v-toolbar>

    <v-data-iterator
      :items="items"
      :items-per-page.sync="itemsPerPage"
      :page="page"
      :search="search"
      :sort-by="sortBy.toLowerCase()"
      :sort-desc="sortDesc"
      hide-default-footer
    >
      <template v-slot:header>
        <v-toolbar
          dark
          color="blue darken-3"
          class="mb-1"
        >
          
          <template v-if="true">
            <v-select
              v-model="sortBy"
              flat
              solo-inverted
              hide-details
              :items="keys"
              prepend-inner-icon="search"
              label="Sort by"
            ></v-select>
            <v-spacer></v-spacer>
            <v-btn-toggle
              v-model="sortDesc"
              mandatory
            >
              <v-btn
                large
                depressed
                color="blue"
                :value="false"
              >
                <v-icon>mdi-arrow-up</v-icon>
              </v-btn>
              <v-btn
                large
                depressed
                color="blue"
                :value="true"
              >
                <v-icon>mdi-arrow-down</v-icon>
              </v-btn>
            </v-btn-toggle>
          </template>
        </v-toolbar>
      </template>



       <v-list >

         <v-list-item>
         
        <v-list-item-content>
          <v-list-item-title class='lista-header' >Fecha</v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title class='lista-header' >Estado</v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title class='lista-header'  >Nombre</v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title class='lista-header' >Duración</v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title class='lista-header' >Región</v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title class='lista-header' >Comuna</v-list-item-title>
        </v-list-item-content>

          
      </v-list-item>

 <v-dialog v-model="dialogEdit" persistent max-width="600px">
   <template  v-slot:activator="{ on, attrs }">
      <v-list-item     
        v-for="item in items"
        :key="item.rId"    
        v-bind="attrs"
        v-on="on"       
      >
       
        <v-list-item-content>
          <v-list-item-title  v-text="item.fecha"></v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title v-text="item.estado"></v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title style="text-align: left" v-text="item.nombre"></v-list-item-title>
        </v-list-item-content>

         <v-list-item-content>
          <v-list-item-title v-text="item.duracion"></v-list-item-title>
        </v-list-item-content>

        <v-list-item-content>
          <v-list-item-title v-text="item.region"></v-list-item-title>
        </v-list-item-content>

        <v-list-item-content>
          <v-list-item-title v-text="item.comuna"></v-list-item-title>
        </v-list-item-content>
   
      </v-list-item>
      </template>
       <modal-movimiento class='md-2' 
       :itemsPadre="items" 
       :accion='agregar' 
       @masMovimientos="actualizaItems" 
       />
      </v-dialog>
    </v-list>
    </v-data-iterator>
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
       <modal-movimiento class='md-2' 
       :itemsPadre="items" 
       @masMovimientos="actualizaItems" 
       :accion='agregar' 
       />
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
      cargaInicial(){
        this.items = [
          { rId:'1', estado:"En Bruto",fecha:"01-06-2020",nombre:"nombre 1",duracion:"130",region:"RM",comuna:"santiago"},
          { rId:'2', estado:"Transcrito",fecha:"02-06-2020",nombre:"nombre muy muy largo por que si",duracion:"59",region:"RM",comuna:"santiago"},
          { rId:'3', estado:"Publicado",fecha:"03-06-2020",nombre:"otro nombre",duracion:"41",region:"RM",comuna:"santiago"},
          { rId:'4', estado:"Publicado",fecha:"04-06-2020",nombre:"otro nombre",duracion:"43",region:"RM",comuna:"santiago"},
          { rId:'5', estado:"En Bruto",fecha:"04-06-2020",nombre:"otro nombre2",duracion:"44",region:"RM",comuna:"santiago"},
          { rId:'6', estado:"En Bruto",fecha:"20-06-2020",nombre:"nombre 2",duracion:"45",region:"RM",comuna:"santiago"},
        ]
      },
      nextPage () {
        if (this.page + 1 <= this.numberOfPages) this.page += 1
      },
      formerPage () {
        if (this.page - 1 >= 1) this.page -= 1
      },
      updateItemsPerPage (number) {
        this.itemsPerPage = number
      },
    
    },

      computed: {
      numberOfPages () {
        return Math.ceil(this.items.length / this.itemsPerPage)
      },
      filteredKeys () {
        return this.keys.filter(key => key !== `estado`)
      },
    },
    
      created(){
        console.log('on create')
        this.cargaInicial()
    },


    data: () => ({
        dialog: false,
        dialog2:false,
        dialogEdit:false,
        items: [],
        editar: 'editar',
        agregar: 'agregar',
        itemsPerPageArray: [4, 8, 12],
        search: '',
        filter: {},
        sortDesc: false,
        page: 1,
        itemsPerPage: 4,
        sortBy: 'name',
        keys: [
          'En Bruto',
          'Publicado',
          'Transcrito'
        ],
    
    }),
  }
</script>

<style scoped>
  .lista-header{
    font-weight: bolder;
    color:black;

  }
</style>