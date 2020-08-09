<template>
  <ion-app>
    <ion-header>
      <ion-toolbar color="primary">
        <ion-title>Vue Capacitor</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content padding>
      The world is over!
      <p>
        git lost at
        <a href="https://ionicframework.com/docs">Ionic Docs</a>!
      </p>
      <ion-button @click="toAboutPage" full>About</ion-button>
      <ion-button @click="showDialogAlert" full>Alert!</ion-button>

      <ion-button
        :style="{ display: addBtnState }"
        @click="add2HomeScreen"
        id="a2hsBtn"
        >Add to home screen</ion-button
      >
    </ion-content>
  </ion-app>
</template>

<script>
import { Plugins } from "@capacitor/core";

let deferredPrompt;
let add2hsBtnDisabled = false;

window.addEventListener("beforeinstallprompt", e => {
  // Prevent Chrome 67 and earlier from automatically showing the prompt
  e.preventDefault();
  // Stash the event so it can be triggered later.
  deferredPrompt = e;
  // Update UI to notify the user they can add to home screen
  add2hsBtnDisabled = false;
});

export default {
  name: "Home",
  computed: {
    addBtnState() {
      return add2hsBtnDisabled ? "block" : "none";
    }
  },
  methods: {
    toAboutPage() {
      this.$router.push("about");
    },
    async showDialogAlert() {
      await Plugins.Modals.alert({
        title: "Alert",
        message: "This is an example alert box"
      });
    },
    add2HomeScreen() {
      // hide our user interface that shows our A2HS button
      add2hsBtnDisabled = true;
      // Show the prompt
      deferredPrompt.prompt();
      // Wait for the user to respond to the prompt
      deferredPrompt.userChoice.then(choiceResult => {
        if (choiceResult.outcome === "accepted") {
          console.log("User accepted the A2HS prompt");
          Plugins.Modals.alert({
            title: "A2HS",
            message: "YAS!"
          }).then(console.info, console.error);
        } else {
          console.log("User dismissed the A2HS prompt");
        }
        deferredPrompt = null;
      });
    }
  }
};
</script>
