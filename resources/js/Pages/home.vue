<template>
<v-theme-provider theme="light" with-background class="pa-5">
    <v-container>
    <v-row justify="space-around">
        <v-card width="400" height="630" class="mt-2">
        <v-img height="200" src="https://farmalkes.kemkes.go.id/wp-content/uploads/2020/11/kip.png" cover></v-img>
        <v-card-text>
            <div class="font-weight-bold ms-1 mb-2 text-center">
                <br><h1>Masuk</h1><br>
            </div>
            <v-form>
                <v-text-field append-inner-icon="mdi mdi-account" variant="solo" label="Username" v-model="form.username" :error-messages="errors.username"></v-text-field>
                <v-text-field append-inner-icon="mdi mdi-account-key" variant="solo" label="Password" type="password" v-model="form.password" :error-messages="errors.password"
                ></v-text-field>
                    <br><v-btn block color="brown" @click="login">Masuk</v-btn>
                <div class="mt-5">
                    <v-btn block small x-small @click="register">Daftar</v-btn>
                </div>
            </v-form>
        </v-card-text>
      </v-card>
    </v-row>
  </v-container>
</v-theme-provider>
</template>

<script>
import {router} from '@inertiajs/vue3'
export default {
props:{
    errors:Object
},
    data(){
        return{
            form:{
                username:"",
                password:"",
            }
        }
    },
    methods:{
        login(){
            router.post('/login', this.form)
        },
        register(){
            router.get('/register')
        }
    },


};
</script>

<style></style>
