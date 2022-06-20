<template>
    <v-app>
      <v-container>
        <v-card>
          <v-card-title>
            COMMENTS
            <v-spacer></v-spacer>
          </v-card-title>
            <div class="mb-6 pl-2 pr-2">
                <v-alert
                v-if="mostrar"
                dense
                text
                type="success"
                >
                Se filtro correctamente
                </v-alert>    
                <v-alert
                v-if="mostrar"
                dense
                border="left"
                type="warning"
                >
                NO TE OLVIDES DE PULSAR 'MOSTRAR TODOS' PARA UN NUEVO FILTRO
                </v-alert>
                <v-row>
                    <v-col cols="12" md="10">
                        <v-select
                        :items="selectArray"
                        @input="filterEmail"
                        v-model="emailDominioSelect"
                        label='Dominio'>
                        </v-select>
                    </v-col>
                    <v-col cols="12" md="1">
                        <v-btn @click="refres()"> Mostrar Todos
                        </v-btn>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col cols="12">
                        <v-expansion-panels>
                            <v-expansion-panel
                                v-for="(comment,i) in comments" :key="i"
                            > 
                            <v-col cols="12" md="8">
                            <v-chip color="rgb(144, 235, 212)">{{comment.id}}</v-chip>
                            </v-col>
                            <v-expansion-panel-header>
                                <v-card-title
                                v-text="comment.email"
                                >
                                </v-card-title>
                                {{comment.name}}
                            </v-expansion-panel-header>
                            <v-expansion-panel-content class="deco2">
                                {{comment.body}}
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
    data() {
        return {
            comments:[],
            selectArray:[],
            emailDominioSelect:'',
            mostrar:false
        }
    },
    methods: {
        getComments(){
            this.axios('/comments')
            .then(res => {
                this.comments = res.data
                this.valueSelectList()
            })
            .catch(e => {
                console.log(e.response)
            })
        },
        filterEmail(){
            this.comments = this.comments.filter(comment => this.formatEmail(comment.email) === this.emailDominioSelect)
            this.mostrar=true
        },
        formatEmail(email){
            const emailFormat = email.substring(email.indexOf('@'))
            return emailFormat.substring(emailFormat.indexOf('.'))
        },
        refres(){
            this.mostrar=false
            this.getComments()  
        },
    },
    computed:{
        valueSelectList(){
        const dominios = []
        this.comments.forEach(comment => dominios.push(this.formatEmail(comment.email)))
        this.selectArray = [...new Set(dominios)]
        },
    },
    created() {
        this.getComments()
    },   
}
</script>
<style lang="">
    
</style>