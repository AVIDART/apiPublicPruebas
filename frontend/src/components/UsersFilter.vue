<template lang="">
    <v-row>
        <v-col cols="12" md="5">
            <v-text-field
            v-model="nombre"
            label="Buscar"
            type=string
            >
            </v-text-field>
        </v-col>         
        <v-col cols="12" md="3"> 
            <v-select
            :items="selectArray"
            v-model="nombre">
            </v-select> 
        </v-col> 
        <v-col cols="12" md="2">
            <v-btn block @click="filtrar">Filtrar</v-btn> 
        </v-col>          
        <v-col cols="12" md="2"> 
            <v-btn block @click="reiniciar">Reiniciar</v-btn> 
        </v-col>                       
    </v-row>
</template>
<script>
export default {
    props:{
        selectArray:Array
    },
    data() {
        return {
            nombre:''
        }
    },
    methods: {
        getUsers(){
            this.$emit('getUsers')
        },
        filtrar(){
            this.$emit('filter',this.nombre)
        },
        reiniciar(){
            this.getUsers()
            this.nombre = ''
        },
    },
    created() {
        this.getUsers()
    },
}
</script>
<style lang="">
    
</style>