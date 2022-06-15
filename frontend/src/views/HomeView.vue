<template>
    <v-app>
      <v-container>
        <v-card>
          <v-card-title>
            POSTS
            <v-spacer></v-spacer>
          </v-card-title>
            <div class="mb-6 pl-2 pr-2">
              <v-row>
                <v-col cols="12" md="5">
                  <v-text-field
                  v-model="nombre"
                  label="Nomber"
                  type=string
                  >
                  </v-text-field>  
                </v-col>
                <v-col cols="12" md="3">
                  <v-text-field
                  v-model="id"
                  label="ID"
                  type=number
                  >
                  </v-text-field>
                </v-col>
                <v-col cols="12" md="2" class="text-center">
                    <v-btn @click="getUsers" block color="#0BB88E">USERS</v-btn>
                </v-col>                 
                <v-col cols="12" md="2" class="text-center">
                    <v-btn @click="getPost(id)" block color="#0BB88E">ID</v-btn>                  
                </v-col>  
              </v-row>
              <v-row>
                <v-col cols="12" class="text-center">
                    <v-btn @click="$router.push('posts')" block color="#0BB02E">PUBLICAR UN POST</v-btn>                  
                </v-col>  
              </v-row>
              <v-data-table
                :search="nombre"
                itemKey="id"
                :items="datos"
                :headers="headers">
              </v-data-table>
              <v-row v-if="existe" justify="center">
                <v-col cols="12">
                  <v-subheader>PUBLICADOS</v-subheader>                                     
                  <v-expansion-panels class="mb-6">
                    <v-expansion-panel>
                      <v-expansion-panel-header class="deco">
                          <v-row>
                            <strong v-html="postTitulo"></strong> 
                            <v-img :src= avatar></v-img>
                          </v-row>
                      </v-expansion-panel-header>
                      <v-expansion-panel-content class="deco2">
                        {{post.body}}
                      </v-expansion-panel-content>
                    </v-expansion-panel>
                  </v-expansion-panels>
                </v-col>
              </v-row>
            </div>           
        </v-card>
      </v-container>
    </v-app>
</template>

<script>


  export default {
    name: 'Home',

    components: {
     
    },
    data() {
      return {
        nombre:"",
        id:null,
        avatar:'',
        datos:[],
        post:[],
        postTitulo:'',
        existe:false,
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
      getPost(id){
        this.axios.get(`/posts/${id}`)
          .then(res => {
            console.log(res)
            this.post = res.data
            this.postTitulo = res.data.title
            this.existe = true
            this.avatar=this.getPhoto()
          })
          .catch(e => {
            console.log(e.response)
          })
      },     
      getPhoto(){
        this.axios.get('/photos')
          .then(res => {
            console.log(res.data[this.id].thumbnailUrl)
            return res.data[this.id].thumbnailUrl
          })
          .catch(e => {
            console.log(e.response)
          })
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
