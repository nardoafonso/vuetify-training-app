<template>
    <v-dialog max-width="600px" v-model="dialog">
        <template v-slot:activator="{ on }">
        <v-btn color="success" dark v-on="on">Add a new project</v-btn>
      </template>
       <v-card>
            <v-card-title>
                <h2>Add a new project</h2> 
            </v-card-title>
            <v-card-text>
                <v-form @submit.prevent="submit" class="px-3" ref="form">
                    <v-text-field label="Title" v-model="title" prepend-icon="mdi-folder" :rules="inputRules"></v-text-field>
                    <v-textarea label="Information" v-model="content" prepend-icon="mdi-pencil" :rules="inputRules"></v-textarea>
                    <v-menu max-width="290">
                        <template v-slot:activator="{ on }">
                            <v-text-field :value="formatedDate" label="Duo date" :rules="inputRules"
                                prepend-icon="mdi-calendar-range" readonly v-on="on"></v-text-field>
                        </template>
                        <v-date-picker v-model="due" no-title scrollable>
                        </v-date-picker>
                    </v-menu>
                    <v-btn text class="success mx-0 mt-3" type="submit" :loading="loading">Add Project</v-btn>
                </v-form>
            </v-card-text>
        </v-card>
    </v-dialog>
</template>
<script>

import format from 'date-fns/format';
import parseISO from 'date-fns/parseISO'
import { setTimeout } from 'timers';

export default {
    data(){
        return {
            title:'',
            content:'',
            due:null,
            dialog:false,
            loading:false,
            inputRules:[
                v=>v.length>=3 || 'Minimum Length is 3 characteres' 
            ]
        }
    },
    methods:{
        submit(){
            if(this.$refs.form.validate()){
                this.loading = true;
                setTimeout(()=>{
                    console.log(this.title,this.content);
                    this.loading = false;
                    this.dialog = false;
                    this.$emit('closedPopUpEvent');
                },2000)
            }
        }
    },
    computed:{
        formatedDate(){
            return this.due ? format(parseISO(this.due), 'do MMM yyyy') : '';
        }
    }
}
</script>
