<template lang="">
    <v-row>
        <v-alert
            shaped
            dense
            text
            type="success"
        > ACCIÓN EJECUTADA
        </v-alert> 
        <v-alert
            shaped
            dense
            text
            type="success"
        > Titulo: {{nuevoPost.titulo}} | Descripcion: {{nuevoPost.descripcion}}
        </v-alert>
    </v-row>
</template>
<script>
export default {
    props:{
        nuevoPost:Object
    }   
}
</script>
<style lang="">
    
</style>