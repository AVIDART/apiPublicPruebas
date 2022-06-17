<template>
    <v-app-bar
     v-if="isNotLogin()"
      app
      color="#0BB88E"
    >
    <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="../img/libro.png"
          transition="scale-transition"
          width="60"
        />
    </div>
      <v-spacer></v-spacer>
      <v-btn text @click="goToRoute('posts')"> BLOG</v-btn>
      <v-btn text @click="goToRoute('home')"> USERS</v-btn>
      <v-btn text @click="goToRoute('comments')">COMENTARIOS</v-btn>
    </v-app-bar>
</template>

<script>

export default {
  methods: {
    isNotLogin(){
      return this.$route.name != "login"
      
    },
    goToRoute(route){
      if(this.$route.name != route)
        this.$router.push({name:route});
    }
  },
}
</script>