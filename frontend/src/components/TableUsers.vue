<template lang="">
    <v-data-table
    :search="nombre"
    itemKey="id"
    :items="datos"
    :headers="headers">
    </v-data-table>
</template>
<script>
export default {
    props:{
        nombre:String,
        datos:Array,
        headers:Array
    }
    
}
</script>
<style lang="">
    
</style>