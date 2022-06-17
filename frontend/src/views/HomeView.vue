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
              <button-public/>
              <table-users
              :nombre="nombre"
              :datos="datos"
              :headers="headers"
              >
              </table-users>
            </div>           
        </v-card>
      </v-container>
    </v-app>
</template>

<script>
import UsersFilter from "../components/UsersFilter.vue"
import ButtonPublic from "../components/ButtonPublic.vue"
import TableUsers from "../components/TableUsers.vue"
  export default {
    name: 'Home',
    components: {
      UsersFilter,ButtonPublic,TableUsers
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
