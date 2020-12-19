<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Postal Code</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <div v-if="pinSearch">
      <pin-code-search @get-info="getPinInfo" :processing="fetching"/>
      </div>
      <div v-else>
        <branch-name-search @get-info="getBranchInfo" :processing="fetching"/>
      </div>
      <ion-button v-on:click="handleClick" color="dark" fill="outline" expand="block">{{text}}</ion-button>
      <div v-if="info">
        <div v-if="info.PostOffice">
          <ion-button @click="clearInfo" color="dark" expand="block" fill="outline">Clear</ion-button>
          <pin-info  v-for="(i,index) in info.PostOffice" :key="index" :info="i" />
        </div>
        <div v-else>{{info.Message}}</div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, alertController,IonButton  } from '@ionic/vue'
import PinInfo from '../components/PinInfo.vue'
import PinCodeSearch from '../components/PinCodeSearch.vue'
import BranchNameSearch from "../components/BranchNameSearch.vue"

export default {
  name: 'Home',
  components:{
    "ion-page":IonPage,
    "ion-header":IonHeader,
    "ion-toolbar":IonToolbar,
    "ion-content":IonContent,
    "ion-title":IonTitle,
    IonButton,
    PinCodeSearch,
    PinInfo,
    BranchNameSearch
 
  },
  data(){
    return {
        info:null,
        pinSearch:true,
        text:"Search with branch name",
        fetching:false
    }
  },
  methods:{
    handleClick()
    {
      this.pinSearch = !this.pinSearch
      this.text = this.pinSearch ? "Search with branch name" : "Search with pin code"
    },
    getPinInfo(data)
    {
      this.fetching=true
      fetch(`https://api.postalpincode.in/pincode/${data}`)
      .then((res) => {
          if(res.status!==200)
          {
            throw new Error('Network response was not ok');
          }
          return res.json()
      })
      .then(jsonRes => {
        this.info = jsonRes[0];
        this.fetching = false
      })
      .catch((err)=>{
          // alert(err)
          this.showAlert(err)
      });

      
    },

    getBranchInfo(data)
    {
      this.fetching = true
      fetch(`https://api.postalpincode.in/postoffice/${data}`)
      .then((res) => {
          if(res.status!==200)
          {
            throw new Error('Network response was not ok');
          }
          return res.json()
      })
      .then(jsonRes => {
        this.info = jsonRes[0];
        this.fetching = false
      })
      .catch((err)=>{
          // alert(err)
          this.showAlert(err)
      });

      
    },

    async showAlert(err)
    {
      const alert = await alertController
        .create({
          header: "Try again later",
          message:err,
          buttons:['OK']
        });
        return alert.present();
    },

    clearInfo()
    {
      this.$router.go()
    }
  }
 
}
</script>
