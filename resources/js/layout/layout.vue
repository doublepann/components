<template>

<v-theme-provider theme="light" with-background class="pa-10">
    <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" >

       <v-list density="compact">
      <v-list-subheader>{{user.nama}}</v-list-subheader>
        <Link href="/admin" as="div">

      <v-list-item
        active-color="primary"
        to="/admin">
        <template v-slot:prepend>
          <v-icon icon="mdi mdi-view-dashboard"></v-icon>
        </template>

        <v-list-item-title>Dashboard</v-list-item-title>
      </v-list-item>
      </Link>
      <Link v-if="user.level=='admin'" href="/admin/user" as="div">
      <v-list-item active-color="primary" to="/admin/user">
        <template v-slot:prepend>
          <v-icon icon="mdi mdi-account-group"></v-icon>
        </template>

        <v-list-item-title>User</v-list-item-title>
      </v-list-item>
      </link>
      <Link v-if="user.level=='admin'" href="/admin/register" as="div">
      <v-list-item active-color="primary" to="/admin/user">

        <template v-slot:prepend>
          <v-icon icon="mdi mdi-account-group"></v-icon>
        </template>

        <v-list-item-title>User Register</v-list-item-title>
      </v-list-item>
      </link>
    </v-list>

    <template v-slot:append>
        <div class="pa-2">
        <v-btn block @click="logout" color="red" prepend-icon="mdi mdi-logout">logout</v-btn>
        </div>
    </template>

    </v-navigation-drawer>


    <v-main>
      <v-container>
        <slot/>
      </v-container>
    </v-main>
  </v-app>
</v-theme-provider>
</template>

<script>
import {router, Link} from '@inertiajs/vue3'
export default {
    components:{
        Link
    },
        data: () => ({ drawer: null }),
        computed:{
            user(){
                return this.$page.props.auth.user
            }
        },
        methods:{
            logout(){
            router.get("/logout")
            },
        },
};
</script>

<style>

</style>
