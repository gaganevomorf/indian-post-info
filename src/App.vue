<template>
  <div id="app">
    <ion-app>
      <ion-vue-router/>
    </ion-app>
  </div>
  
</template>

<script>
import {IonApp, IonRouterOutlet} from '@ionic/vue'
export default {
  components:{
    "ion-app":IonApp,
    "ion-vue-router":IonRouterOutlet
  }
}
</script>
