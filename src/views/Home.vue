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
    </ion-content>
  </ion-app>
</template>

<script>
export default {
  name: "Home",
  methods: {
    toAboutPage() {
      this.$router.push("about");
    }
  }
};
</script>
