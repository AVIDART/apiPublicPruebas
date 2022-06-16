<template lang="">
    <v-app>
        <v-container>
            <v-card-title>
                POSTS
            <v-spacer></v-spacer>
          </v-card-title>
            <div class="mb-6 pl-2 pr-2">
                <v-row>
                    <v-alert v-if="alerta"
                        shaped
                        dense
                        text
                        type="success"
                    > ACCIÓN EJECUTADA
                    </v-alert> 
                    <v-alert v-if="alerta"
                        shaped
                        dense
                        text
                        type="success"
                    > Titulo: {{nuevoPost.titulo}} | Descripcion: {{nuevoPost.descripcion}}
                    </v-alert>
                </v-row>
                <v-row v-if="mostrar">
                    <v-col
                        cols="12"
                        md="4"
                    >
                        <v-text-field
                        v-model="nuevoPost.titulo"
                        :counter="10"
                        label="Titulo"
                        required
                        ></v-text-field>
                    </v-col>

                    <v-col
                        cols="12"
                        md="4"
                    >
                        <v-text-field
                        v-model="nuevoPost.descripcion"
                        :counter="10"
                        label="Descripcion"
                        required
                        ></v-text-field>
                    </v-col> 
                    <v-col
                        cols="12"
                        md="2"
                    >
                        <v-btn block color="rgb(144, 235, 212)" @click="addPost()">ADD</v-btn>
                    </v-col>      
                    <v-col
                        cols="12"
                        md="2"
                    >
                        <v-btn block color="rgb(255, 130, 0)" @click="editPost()">EDIT</v-btn>
                    </v-col>
                    </v-row>
                <v-row>
                    <v-col cols="12">
                        <v-btn block color="rgb(144, 235, 212)" @click="mostrar=true">QUIERO AGREGAR UN POST</v-btn>
                        <v-expansion-panels>
                            <v-expansion-panel
                                v-for="(post,i) in posts" :key="i"
                            > 
                            <v-chip color="rgb(144, 235, 212)">{{post.id}}</v-chip>
                            <v-col align=right>                    
                                <v-btn @click="delPost(post.id)" color="rgb(242, 19, 93)">Eliminar</v-btn> |
                                <v-btn @click="editOne(post.id,post.userId)" color="rgb(255, 130, 0)">Editar</v-btn>
                            </v-col> 
                            <v-expansion-panel-header>
                                {{post.title}}
                            </v-expansion-panel-header>
                            <v-expansion-panel-content class="deco2">
                                {{post.body}}
                            </v-expansion-panel-content>
                            </v-expansion-panel>
                        </v-expansion-panels>
                    </v-col>
                </v-row>
            </div>
        </v-container>
    </v-app>
</template>
<script>
export default {
    data() {
        return {
            posts:[],
            alerta:false,
            mostrar:false,
            nuevoPost:{titulo:'', descripcion:'',usuarioID:0},
            idEdit:0,       
        }
    },
    methods: {
        getPosts(){            
            this.axios.get('/posts')
            .then(res => {
                this.posts = res.data
            })
            .catch(e => {
                console.log(e.response)
            })     
            },
        delPost(id){
            this.axios.delete(`/posts/${id}`)
            .then(res => {
                this.alerta=true
                console.log(res)
            })
            .catch(e => {
                console.log(e.response)
            })   
        },   
        addPost(){
            this.axios.post('/posts/',this.nuevoPost)
            .then(res => {   
                console.log(res)
                this.alerta=true
            })
            .catch(e => {
                console.log(e.response)
            })   
        },       
        editPost(){
            this.axios.put(`/posts/${this.idEdit}`,this.nuevoPost)
            .then(res => {   
                console.log(res)
                this.alerta=true
            })
            .catch(e => {
                console.log(e.response)
            })   
        },
        editOne(id,useid){
            this.mostrar=true
            this.idEdit=id
            this.nuevoPost.usuarioID=useid
        },
        guardarid(idusuario){
                console.log(idusuario)
        }      
    },
    created() {
        this.getPosts()
    },
    
}
</script>
<style lang="">
    
</style>