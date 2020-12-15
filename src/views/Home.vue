<template>
  <div id="Home">    
    <v-container>    
    <!-- +-------------------------------------------------------------------+
        |                           NAVEGACION                               |
        +-------------------------------------------------------------------+ -->        
    <v-row>
      <v-bottom-navigation>
        <div class="mt-2">
          <v-btn @click="router_children(1)">
            <span>Ver Enfermeras</span>
            <v-icon color="primary">mdi-account-search</v-icon>
          </v-btn>
          <v-btn @click="router_children(2)">
            <span>Agregar Enfermera</span>
            <v-icon color="primary">mdi-account-plus</v-icon>
          </v-btn>
        </div>
      </v-bottom-navigation>
    </v-row>
    <!-- +-------------------------------------------------------------------+
        |                ESPACACIO PARA RUTA HIJAS                          |
        +-------------------------------------------------------------------+ --> 
    <router-view></router-view>   
  </v-container>
  </div>
</template>

<script>
const ENUM_ROURTER = Object.freeze({
  TablaEnfermeras: 1,
  AgregarEnfermera: 2,
})
export default {
  name: "Home",
  data: () => ({
    subVistaSelect: true,           
    
  }),

// +----------------------------------------------------------+
// |                    CICLOS DE VIDA                        |
// +----------------------------------------------------------+
  beforeMount() {
  
  },
// +----------------------------------------------------------+
// |                        METODOS                           |
// +----------------------------------------------------------+
  methods: {
    router_children(_enum_router){
      console.log(_enum_router)
      if(ENUM_ROURTER.TablaEnfermeras === _enum_router){
        this.$router.push('/TablaEnfermeras')
      }
      if(ENUM_ROURTER.AgregarEnfermera === _enum_router){
        this.$router.push('/AgregarEnfermera')
      }      
    }, 
  }
};
</script>
