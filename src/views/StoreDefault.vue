<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
            <ion-back-button default-href="/tabs/tab2"></ion-back-button>
        </ion-buttons>
        <ion-title>StoreDefault</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">StoreDefault</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-card>
        <ion-card-content>
          <Suspense>
            <template #default>
              <DefaultTest />
            </template>
            <template #feedback>
              <div> Loading ... </div>
            </template>
          </Suspense>
        </ion-card-content>
      </ion-card>
    </ion-content>
  </ion-page>
</template>
<script lang="ts">
import { IonPage, IonButtons, IonHeader, IonToolbar, IonBackButton,
        IonTitle, IonContent, IonCard, IonCardContent } from '@ionic/vue';
import { defineComponent } from 'vue';
import DefaultTest from '@/components/DefaultTest.vue';
export default defineComponent({
  name: 'StoreDefault',
  components: { IonPage, IonButtons, IonHeader, IonToolbar, IonBackButton,
        IonTitle, IonContent, IonCard, IonCardContent, DefaultTest }
});
</script>
<style>
h1 {
    text-align: center;
}
</style>