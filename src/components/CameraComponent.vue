<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Camera</ion-card-title>
    </ion-card-header>

    <ion-card-content>

      <ion-button expand="block" @click="takePicture">
        <ion-icon slot="start" :icon="cameraIcon"></ion-icon>
        Take Picture
      </ion-button>

      <ion-text v-if="errorMessage" color="danger">
        <p>{{ errorMessage }}</p>
      </ion-text>

    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">

import {
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonButton,
  IonIcon,
  IonText
} from '@ionic/vue';

import { camera as cameraIcon } from 'ionicons/icons';

import {
  Camera,
  CameraResultType,
  CameraSource
} from '@capacitor/camera';

import { ref } from 'vue';

const errorMessage = ref('');

/*
 * Ipapadala nito ang captured photo
 * papunta sa parent component (HomePage.vue)
 */
const emit = defineEmits<{
  (event: 'photo-taken', photo: string): void;
}>();

const takePicture = async () => {

  try {

    errorMessage.value = '';

    const image = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.DataUrl,
      source: CameraSource.Camera
    });

    console.log('Photo taken:', image.dataUrl);

    // I-send ang photo sa HomePage.vue
    if (image.dataUrl) {
      emit('photo-taken', image.dataUrl);
    }

  } catch (error) {

    console.error(error);

    errorMessage.value = 'Unable to take picture.';

  }

};

</script>