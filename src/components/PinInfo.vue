<template>
    <ion-card v-if="info">
        <ion-card-header>
            <ion-card-subtitle>{{info.BranchType}}</ion-card-subtitle>
            <ion-card-title>{{info.Name}}</ion-card-title>
            <ion-card-subtitle>{{info.Description}}</ion-card-subtitle>
            
            
        </ion-card-header>
        <ion-card-content>
            <ion-list>
                <ion-item>
                    <ion-label><strong>DeliveryStatus:</strong>{{info.DeliveryStatus}}</ion-label>
                </ion-item>
                <ion-item>
                    <ion-label><strong>Circle:</strong>{{info.Circle}}</ion-label>
                </ion-item>
                <ion-item>
                    <ion-label><strong>District:</strong>{{info.District}}</ion-label>
                </ion-item>
                <ion-item>
                    <ion-label><strong>Division:</strong>{{info.Division}}</ion-label>
                </ion-item>
                <ion-item>
                    <ion-label><strong>Region:</strong>{{info.Region}}</ion-label>
                </ion-item>
                <ion-item>
                    <ion-label><strong>State:</strong>{{info.State}}</ion-label>
                </ion-item>
            </ion-list>
        </ion-card-content>
    </ion-card>
</template>

<script>
import {IonCard,IonCardHeader,IonCardSubtitle,IonCardTitle,IonCardContent,IonItem,IonLabel,IonList} from '@ionic/vue'
export default {
    name:"PinInfo",
    props:['info'],
    components:{
        IonCard,IonCardHeader,IonCardSubtitle,IonCardTitle,IonCardContent,IonItem,IonLabel,IonList
    }
}
</script>