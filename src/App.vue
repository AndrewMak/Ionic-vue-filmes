<template>
  <ion-app>
    <div id="nav">
      <ion-toolbar color="primary">       
        <ion-title @click="goToTitle">
          Ionic Top Filmes
        </ion-title>
      </ion-toolbar>
    </div>
    <ion-content color="tint">
      <router-view/>
    </ion-content>
  </ion-app>
</template>

<script>
export default {
  methods: {
    goToTitle() {
      this.$router.push('/')
    },
    goToAbout() {
      this.$router.push('about')
    }
  }
}
</script>