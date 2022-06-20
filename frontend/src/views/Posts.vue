<template lang="">
    <v-app>
        <v-container>
            <v-card-title>
                POSTS
            <v-spacer></v-spacer>
          </v-card-title>
            <div class="mb-6 pl-2 pr-2">
                <alertas v-if="alerta"
                :nuevoPost="nuevoPost"
                >
                </alertas>
                <v-select
                :items="selectArray"
                @input="filterPostUserID"
                v-model="userIdSelect">
                </v-select>
                <agregar-post
                v-if="mostrar"
                :nuevoPost="nuevoPost"
                @addPost="addPost"
                @editPost="editPost"
                >
                </agregar-post>
                <table-post
                @mostrarFuntion="mostrarFuntion"
                :posts="posts"
                @delPost="delPost"
                @editOne="editOne"
                >
                </table-post>
            </div>
        </v-container>
    </v-app>
</template>
<script>
import Alertas from "../components/Alertas.vue"
import TablePost from "../components/TablePost.vue"
import AgregarPost from "../components/AgregarPost.vue"
export default {
    components:{
        Alertas,TablePost,AgregarPost
    },
    data() {
        return {
            userIdSelect:0,
            selectArray:['ALL'],
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
                this.valueSelectList()
            })
            .catch(e => {
                console.log(e.response)
            })     
            },        
        getPost(id){            
            this.axios.get(`/posts/${id}`)
            .then(res => {
                this.nuevoPost.titulo = res.data.title
                this.nuevoPost.descripcion = res.data.body
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
            this.getPost(this.idEdit)
        },
        mostrarFuntion(mostrar){
               this.mostrar=mostrar
        },
        filterPostUserID(){
            if (this.userIdSelect === 'ALL'){
                this.getPosts()
            }
            else
                this.posts = this.posts.filter(post => post.userId === this.userIdSelect)
                this.selectArray.splice(1)
        }    
    },
    created() {
        this.getPosts()
    },
    computed:{
      valueSelectList(){
        this.posts.forEach(element => this.selectArray.push(element.userId))
      }
    },
    
}
</script>
<style lang="">
    
</style>