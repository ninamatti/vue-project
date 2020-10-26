<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>{{ title }}</h1>
    
    <navbar  v-on:change-view="changeView"/>
    <allphotos v-if="currentView === 'AllPhotos'"/>
    <singlephoto v-else />
  </div>
</template>

<script>
import AllPhotos from './components/AllPhotos.vue';
import Navbar from "./components/Navbar";
import SinglePhoto from "./components/SinglePhoto";
import { listObjects } from "../utils/index.js";


export default {
  name: "App",
  components: {
    navbar: Navbar,
    allphotos: AllPhotos,
    singlephoto: SinglePhoto,
  },
  data: () => ({
    title: "Photo Upload App",
    currentView: 'SinglePhoto',
    photos: [],
    selectedPhoto: "image",
  }),
  created() {
    console.log('At this point, this.property is now reactive and propertyComputed will update.')
    this.property = 'Example property updated.'
    //// sets this.photos to array of keys
    listObjects()
    .then((data) => {
     return data.map((photo)=> photo.Key);
    }).then((keysArr) => {
      console.log(keysArr);
      this.photos = keysArr;
    });
    /////
  },
  methods: {
    changeView: function(newValue) {
      this.currentView = newValue;
    }
  }
};
</script>

<style>
#app {
  text-align: center;
}
</style>
