<template lang="">
  <v-row>
        <v-col
            cols="12"
            md="4"
        >
            <v-text-field
            hint="Escriba el titulo nuevo"
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
            <v-textarea
            hint="Escriba la descripción nueva"
            v-model="nuevoPost.descripcion"
            label="Descripcion"
            required
            ></v-textarea>
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
</template>
<script>
export default {
    props:{
        nuevoPost:Object,
        defaultTItle:String,
        defaultDescription:String
    },
    methods: {
        addPost(){
            this.$emit('addPost')
        },        
        editPost(){
            this.$emit('editPost')
        },
    },   
}
</script>
<style lang="">
    
</style>