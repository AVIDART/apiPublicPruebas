<template>
  <v-app>
    <v-app-bar
      app
      color="#0BB88E"
    >
     <navigation-bar/>
    </v-app-bar>
    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>
import NavigationBar from './components/NavigationBar.vue'
export default {
  name: 'App',
  components:{
     NavigationBar
  },
  data: () => ({
    //
  }),
};
</script>
