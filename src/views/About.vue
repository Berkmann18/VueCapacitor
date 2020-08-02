<template>
  <ion-app>
    <ion-header>
      <ion-toolbar color="secondary">
        <ion-title>Vue Capacitor | About</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content padding>
      This is the about page.
      <ion-button @click="toHomePage" full>Home</ion-button>
    </ion-content>
  </ion-app>
</template>

<script>
export default {
  name: "About",
  methods: {
    toHomePage() {
      this.$router.push("/");
    }
  }
};
</script>
