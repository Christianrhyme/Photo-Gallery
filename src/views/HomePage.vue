<template>
  <ion-page>

    <ion-header>
      <ion-toolbar>
        <ion-title>My Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">

      <!-- Camera -->
      <CameraComponent
        @photo-taken="addPhoto"
      />

      <!-- Photo Gallery -->
      <PhotoGallery
        ref="gallery"
      />

    </ion-content>

  </ion-page>
</template>


<script setup lang="ts">

import { ref } from 'vue';

import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent
} from '@ionic/vue';

import CameraComponent from '@/components/CameraComponent.vue';
import PhotoGallery from '@/components/PhotoGallery.vue';


const gallery = ref();


const addPhoto = (photo: string) => {

  gallery.value?.addPhoto(photo);

};

</script>