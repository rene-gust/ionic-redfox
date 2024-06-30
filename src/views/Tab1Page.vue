<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Password Protected Web View</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ion-item>
        <ion-label position="floating">Enter Password</ion-label>
        <ion-input v-on:keyup.enter="checkPassword" v-model="password" type="password"></ion-input>
      </ion-item>
      <ion-button expand="block" @click="checkPassword">Submit</ion-button>
      <ion-toast
          v-if="showToast"
          :message="toastMessage"
          :duration="2000"
          position="top"
          @didDismiss="showToast = false"
      ></ion-toast>
    </ion-content>
  </ion-page>
</template>

<script>
import { defineComponent, ref } from 'vue';
import { InAppBrowser } from '@ionic-native/in-app-browser';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonLabel, IonInput, IonButton, IonToast } from '@ionic/vue';
import config from '../../config.json';

export default defineComponent({
  name: 'Home',
  components: {
    IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonLabel, IonInput, IonButton, IonToast
  },
  setup() {
    const password = ref('');
    const showToast = ref(false);
    const toastMessage = ref('');

    const checkPassword = () => {
      const correctPassword = config.password;
      if (password.value === correctPassword) {
        const browser = InAppBrowser.create('https://x.com', '_self', {
          location: 'no',
          clearcache: 'no',
          clearsessioncache: 'no',
          zoom: 'no',
          hardwareback: 'no',
          mediaPlaybackRequiresUserAction: 'no',
          shouldPauseOnSuspend: 'no',
          closebuttoncaption: 'Close',
          disallowoverscroll: 'no',
          toolbar: 'no',
        });
      } else {
        toastMessage.value = 'Incorrect password!';
        showToast.value = true;
      }
    };

    return {
      password,
      showToast,
      toastMessage,
      checkPassword,
    };
  },
});
</script>

<style scoped>
</style>
