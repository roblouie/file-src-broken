<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <img :src="src"/>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { Capacitor, Filesystem, FilesystemDirectory } from "@capacitor/core";

import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar
  },
  data() {
    return {
      src: ''
    }
  },
  methods: {
    async ionViewWillEnter() {
      const base64Data = 'iVBORw0KGgoAAAANSUhEUgAAABkAAAAbCAYAAACJISRoAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAA'
                  + 'EnQAABJ0Ad5mH3gAAABVSURBVEhLtcgxFYAwEECxeoKHGKh/G4eBjL9Dlqx1vXMcs8asMWvMGrPGrDFrzBqzxqwxa8was8as'
                  + 'MWvMGrPGrDFrzBqzxqwxa8zaur85bj17ztrzA6hlFRB6JuNPAAAAAElFTkSuQmCC';

      const savedPhotoFile = await Filesystem.writeFile({
        path: "myFile.png",
        data: base64Data,
        directory: FilesystemDirectory.Documents
      });

      const savedPhoto = Capacitor.convertFileSrc(savedPhotoFile.uri);
      this.src = savedPhoto;
    }
  }

  
});
</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>