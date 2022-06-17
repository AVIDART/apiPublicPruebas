<template>
    <v-app>
      <v-container>
        <v-card>
          <v-card-title>
            COMMENTS
            <v-spacer></v-spacer>
          </v-card-title>
          <v-row>
            <div class="mb-6 pl-2 pr-2">
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
            </div> 
        </v-row>          
        </v-card>
      </v-container>
    </v-app>
</template>
<script>
export default {
    data() {
        return {
            comments:[]
        }
    },
    methods: {
        getComments(){
            this.axios('/comments')
            .then(res => {
                this.comments = res.data
            })
            .catch(e => {
                console.log(e.response)
            })
        }
    },
    created() {
        this.getComments()
    },   
}
</script>
<style lang="">
    
</style>