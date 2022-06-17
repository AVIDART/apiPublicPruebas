<template>
    <v-app>
      <v-container>
        <v-card>
          <v-card-title>
            USERS
            <v-spacer></v-spacer>
          </v-card-title>
            <div class="mb-6 pl-2 pr-2">
              <users-filter
              @filter="filter"
              @getUsers="getUsers"
              >
              </users-filter>
              <v-row>
                <v-col cols="12" class="text-center">
                    <v-btn @click="$router.push('posts')" block color="rgb(144, 235, 212)">PUBLICAR UN POST</v-btn>                  
                </v-col>  
              </v-row>
              <v-data-table
                :search="nombre"
                itemKey="id"
                :items="datos"
                :headers="headers">
              </v-data-table>
            </div>           
        </v-card>
      </v-container>
    </v-app>
</template>

<script>
import UsersFilter from "../components/UsersFilter.vue"
  export default {
    name: 'Home',
    components: {
      UsersFilter
    },
    data() {
      return {
        nombre:"l",
        datos:[],
        headers:[{
          text:"ID",
          align:"center",
          value:"id"
        },
        {
          text:"NOMBRE",
          align:"center",
          value:"name"
        },
        {
          text:"USUARIO",
          align:"center",
          value:"username"
        },     
        {
          text:"CIUDAD",
          align:"center",
          value:"address.city"
        },     
        {
          text:"CORREO",
          align:"center",
          value:"email"
        },     
        {
          text:"TELEFONO",
          align:"center",
          value:"phone"
        },    
        ]
      }
    },
    methods: {
      getUsers(){
        this.axios.get('/users')
          .then(res => {
            console.log(res)
            this.datos = res.data
          })
          .catch(e => {
            console.log(e.response)
          })
      },
      filter(nombre2){
        this.nombre=nombre2
      }     
    },
    created() {
      
    },
  }
</script>

<style>

.deco{
  background-color:rgb(144, 235, 212);
}
.deco2{
  background-color:rgb(202, 240, 230);
}

</style>
