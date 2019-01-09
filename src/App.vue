<template>
   <main>
      <v-app>
        <!--<v-content v-if="$store.state.loaded">-->
        <v-content>
          <guest-navigation v-if="role === 'guest'" />
          <admin-navigation v-if="role === 'admin'" />
           <v-container class="mt-3 mb-3 ">

             <!--<v-alert-->
               <!--:type="$store.state.alert.type"-->
               <!--:value="$store.state.alert.show"-->
               <!--&gt;-->
               <!--{{ store.state.alert.message }}-->
             <!--</v-alert>-->

              <router-view  />
          </v-container>
          <app-footer />
        </v-content>
        <!--<container v-else fill-height>-->
          <!--<v-layout flex align-center justify-center>-->
            <!--<v-progress-circular indeterminate :size="100" :width="10" color="purple" />-->
          <!--</v-layout>-->
        <!--</container>-->
      </v-app>
   </main>
</template>

<script>
import AdminNavigation from '@/navigations/admin'
import GuestNavigation from '@/navigations/guest';
import AppFooter from '@/components/Footer';
import {mapGetters} from 'vuex';

export default {
  components:{
      AppFooter,
      GuestNavigation,
      AdminNavigation
  },
  name: 'App',

  computed:{
    ...mapGetters(['role'])
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
