<template>
  <div>
    <auth-form
        action="register"
            v-on:process="register($event)"
    />

    <app-snack-bar
      v-if="snackBar"
      :snack-bar="snackBar"
      :text="message"
      :timeout="timeout"
    />

  </div>
</template>
<script>
import AppSnackBar from '@/components/SnackBar'
import AuthForm from '@/forms/Auth'
import {db}  from '@/main'

export default{
    name: "Register",
    components:{ AuthForm ,AppSnackBar },
    data(){
        return {
            snackBar: false,
            message: '',
            timeout: 5000
        }
    },
    methods:{
      //consultar esta web qui esta la explicacion de cambio en autenticacion
      //https://www.udemy.com/vuejs-2-vuex-firebase-cloud-firestore/learn/v4/t/lecture/11408238?start=0
      register (user) {
           this.$store.dispatch("firebaseRegister", user)
             .then((userRegistered) => {
              const data ={
                uid: userRegistered.user.uid,
                email: user.email,
                role: 'customer'
             };
              db.collection('users').doc(userRegistered.user.uid).set(data).then(()  => {
                this.$store.commit('setRole', data.role);
                this.$router.push('/');
             });
           }).catch((error) => {
             this.message = error.message.substr(0, 340);
             this.snackBar = true;
             setTimeout( () => {
                this.snackBar = false;
             }, this.timeout);
        })
       }
    }
 }
</script>
