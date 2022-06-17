<template lang="">
    <v-row>
        <v-col cols="12">
            <v-btn block color="rgb(144, 235, 212)" @click="mostrar">QUIERO AGREGAR UN POST</v-btn>
            <v-expansion-panels>
                <v-expansion-panel
                    v-for="(post,i) in posts" :key="i"
                > 
                <v-chip color="rgb(144, 235, 212)">{{post.id}}</v-chip>
                <v-col align=right>                    
                    <v-btn @click="delPost" color="rgb(242, 19, 93)">Eliminar</v-btn> |
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
</template>
<script>
export default {
    data() {
        return {
            indicador:true
        }
    },
    props:{
        posts:Array,
    },
    methods: {
        delPost(id){
            this.$emit('delPost',id)
        },        
        editOne(id,userId){
            this.$emit('editOne',id,userId)
        },
        mostrar(){
            this.$emit('mostrarFuntion',this.indicador)
        }
    },
}
</script>
<style lang="">
    
</style>