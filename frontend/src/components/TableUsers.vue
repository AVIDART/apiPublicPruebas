<template lang="">
    <v-data-table

    itemKey="id"
    :items="datos"
    :headers="headers">
        <!-- :search="nombre" -->
    </v-data-table>
</template>
<script>
export default {
    props:{
        // nombre:String,
        datos:Array,
        headers:Array
    }
    
}
</script>
<style lang="">
    
</style>