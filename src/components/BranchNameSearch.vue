<template>
    
    <ion-grid>
        
            <form @submit.prevent="onSubmit">
            <ion-col>
                <ion-item>
                    <ion-label>Branch name:</ion-label>
                    <ion-input 
                    name="branch" 
                    type="text"
                    placeholder="Enter branch name"
                    autofocus="true"
                    clear-input="true"
                    enterkeyhint="search"
                    required="true"
                    maxlength="100"
                    max="100"
                    v-model.trim="branch"
                    
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
    name:"BranchNameSearch",
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
            branch:null,
            lengthError:false
        }
    },
   
    methods:{
        
        onSubmit()
        {
            this.$emit("get-info",this.branch)
        }
    }
}
</script>