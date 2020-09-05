<template>
  <ion-menu content-id="main-content" type="overlay">
    <ion-content>
      <ion-list id="inbox-list">
        <ion-list-header>Inbox</ion-list-header>
        <ion-item lines="none">
          <ion-label>
            <ion-note>hi@ionicframework.com</ion-note>
          </ion-label>
        </ion-item>

        <ion-menu-toggle auto-hide="false" v-for="(p, i) in appPages" :key="i">
          <ion-item
            @click="selectedIndex = i"
            router-direction="none"
            :router-link="p.url"
            lines="none"
            detail="false"
            class="hydrated"
            :class="{ selected: selectedIndex === i }"
          >
            <ion-icon slot="start" :icon="p.icon"></ion-icon>
            <ion-label>{{ p.title }}</ion-label>
          </ion-item>
        </ion-menu-toggle>
      </ion-list>
    </ion-content>
  </ion-menu>
</template>
<script lang="ts">
import {
  IonContent,
  IonIcon,
  IonItem,
  IonLabel,
  IonList,
  IonListHeader,
  IonMenu,
  IonMenuToggle,
  IonNote,
} from "@ionic/vue";
/* Core CSS required for Ionic components to work properly */
import "@ionic/vue/css/core.css";
import { useRoute, useRouter } from "vue-router";
import { defineComponent, ref } from "vue";
import { homeOutline, personOutline, settingsOutline } from "ionicons/icons";

export default defineComponent({
  name: "MainMenu",
  components: {
    IonList,
    IonListHeader,
    IonNote,
    IonContent,
    IonMenu,
    IonMenuToggle,
    IonIcon,
    IonItem,
    IonLabel,
  },
  setup() {
    const selectedIndex = ref(0);
    const appPages = [
      {
        title: "Home",
        url: "/",
        icon: homeOutline,
      },
      {
        title: "Profile",
        url: "/root/profile",
        icon: personOutline,
      },
      {
        title: "Settings",
        url: "/root/settings",
        icon: settingsOutline,
      },
    ];

    const route = useRoute();
    const router  = useRouter()
    

    const path = window.location.pathname.split("/")[1];
    selectedIndex.value = appPages.findIndex(
      (page) => page.title.toLowerCase() === path.toLowerCase()
    );
    console.log("path",path);

    return {
      isSelected: (url: string) => (url === route.path ? "selected" : ""),
      selectedIndex,
      appPages,
      IonList,
      IonListHeader,
      IonNote,
      IonContent,
      IonMenu,
      IonMenuToggle,
      IonIcon,
      IonItem,
      IonLabel,
      homeOutline,
      personOutline,
      settingsOutline,
    };
  },
});
</script>
<style src='@ionic/core/css/core.css'></style>
<style src='@ionic/core/css/ionic.bundle.css'></style>
<style scoped>
.selected {
  --background: rgba(var(--ion-color-primary-rgb), 0.14);
}
</style>