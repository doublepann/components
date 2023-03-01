<template>
<v-theme-provider theme="light" with-background class="pa-10">
    <v-app id="inspire">

    <v-navigation-drawer v-model="drawer">
      <v-sheet color="grey-lighten-4" class="pa-4">

        <div>{{ user.nama }} ({{ user.level }})</div>
      </v-sheet>

      <v-divider></v-divider>

      <v-list>
        <Link href="/masyarakat" as="div">
                <v-list-item to="/masyarakat">
                    <template v-slot:prepend>
                        <v-icon>mdi mdi-home-account</v-icon>
                    </template>

                    <v-list-item-title>Home</v-list-item-title>
                </v-list-item>
                </Link>
                <Link href="/masyarakat/pengaduan" as="div">
                <v-list-item to="/masyarakat">
                    <template v-slot:prepend>
                        <v-icon>mdi mdi-duck</v-icon>
                    </template>

                    <v-list-item-title>Pengaduan</v-list-item-title>
                </v-list-item>
                </Link>
      </v-list>

    </v-navigation-drawer>

    <v-main>
        <v-tooltip text="LOGOUT">
            <template v-slot:activator="{ props }" >
                <v-icon color="red" v-bind="props" @click="logout">mdi mdi-logout</v-icon>
            </template>
        </v-tooltip>
      <v-container class="py-8 px-6" fluid>
        <slot/>
      </v-container>
    </v-main>
  </v-app>
</v-theme-provider>
</template>

<script>
import { Link , router } from '@inertiajs/vue3'
export default {
    components:{
        Link
    },
    data: () => ({
        drawer: null
    }),

    computed:{
            user(){
                return this.$page.props.auth.user
            }
    },

    methods:{
        logout(){
            router.get('/logout')
        }
    }


}
</script>

<style>

</style>
