<template>
  <v-snackbar
    :timeout="timeout"
    :color="color"
    v-model="showSnack" >
    {{ text }}
    <v-btn dark flat @click="showSnack = false">
      {{ $t('messages.close') }}
    </v-btn>
  </v-snackbar>
</template>

<script>
  export default{
    name: "app-bar-snack",
    props: ['snackBar','timeout','text'],
    data(){
      return {
        color: 'primary',
        mode : 'horizontal',
        showSnack : this.snackBar
      }
    }
  }
</script>
