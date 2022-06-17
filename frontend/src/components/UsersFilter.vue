<template lang="">
    <v-row>
        <v-col cols="12" md="10">
            <v-text-field
            v-model="nombre"
            label="Nombre"
            type=string
            >
            </v-text-field>
        </v-col>         
        <v-col cols="12" md="2">
            <v-btn @click="filtrar">Filtrar</v-btn> 
        </v-col>                
    </v-row>
</template>
<script>
export default {
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
    },
    created() {
        this.getUsers()
    },
}
</script>
<style lang="">
    
</style>