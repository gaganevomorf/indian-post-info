<template>
    
    <ion-grid>
        
            <form @submit.prevent="onSubmit">
            <ion-col>
                <ion-item>
                    <ion-label>PIN Code:</ion-label>
                    <ion-input 
                    name="pin" 
                    type="text"
                    placeholder="Enter 6 digit pin code"
                    autofocus="true"
                    clear-input="true"
                    enterkeyhint="search"
                    inputmode="numeric"
                    required="true"
                    maxlength="6"
                    minlength="6"
                    max='6'
                    min="6"
                    v-model.trim="pin"
                    
                    ></ion-input>
                    
                   
                </ion-item>
            </ion-col>

            <ion-col>
                <ion-button color="primary" type="submit" expand="block">
                    <div v-if="processing">
                        <ion-spinner color="light" name="dots"></ion-spinner>
                    </div>
                    <div v-else>
                     Find
                    </div>
                </ion-button>
            </ion-col>
            </form>
        
    </ion-grid>
</template>

<script>
import { IonButton, IonCol, IonGrid, IonInput, IonItem, IonLabel,IonSpinner} from '@ionic/vue'

export default {
    name:"PinCodeSearch",
    props:['processing'],
    components:{
        IonGrid,
        IonCol,
        IonButton,
        IonItem,
        IonLabel,
        IonInput,
        IonSpinner
        
    },
    data: function(){
        return {
            pin:null,
            lengthError:false
        }
    },
   
    methods:{
        
        onSubmit()
        {
            this.pin.toString().length !== 6 
            ?
            this.lengthError=true 
            :
            this.$emit("get-info",this.pin)

        }
    }
}
</script>