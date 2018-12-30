<template>
   <main>
      <v-app>
        <!--<v-content v-if="$store.state.loaded">-->
          <v-content>
          <guest-navigation />
           <v-container class="mt-3 mb-3 ">
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
import GuestNavigation from '@/navigations/guest';
import AppFooter from '@/components/Footer';

export default {
  components:{
      AppFooter,
      GuestNavigation
  },
  name: 'App'
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
