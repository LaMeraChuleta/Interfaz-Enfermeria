<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="align-center">
        <v-app-bar-nav-icon></v-app-bar-nav-icon>
      </div>
      <v-spacer></v-spacer>        
    </v-app-bar>  
    <v-main>    
    <v-container fluid>
      
      <router-view></router-view>
    </v-container>
  </v-main>
  <v-footer color="primary" height="30">    
  </v-footer>
  </v-app>
</template>

<script>


export default {
  name: 'app',
  components: {
    
  },
  data: () => ({
    //
  }),
};
</script>
