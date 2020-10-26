<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>{{ title }}</h1>
    
    <navbar />
    <allphotos v-if="currentView === 'AllPhotos'"/>
    <singlephoto v-else />
  </div>
</template>

<script>
import AllPhotos from './components/AllPhotos.vue';
import Navbar from "./components/Navbar";
import SinglePhoto from "./components/SinglePhoto";

export default {
  name: "App",
  components: {
    navbar: Navbar,
    allphotos: AllPhotos,
    singlephoto: SinglePhoto,
  },
  data: () => ({
    title: "Photo Upload App",
    currentView: 'AllPhotos',
    photos: [],
    selectedPhoto: "image",

  })
};
</script>

<style>
#app {
  text-align: center;
}
</style>
