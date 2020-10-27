<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>{{ title }}</h1>
    
    <navbar  v-on:change-view="changeView"
             v-on:on-upload="updatePhotosAfterUpload"/>
    <allphotos v-if="currentView === 'AllPhotos'" 
    v-bind:photos="photos"/>
    <singlephoto v-else />
  </div>
</template>

<script>
import AllPhotos from './components/AllPhotos.vue';
import Navbar from "./components/Navbar";
import SinglePhoto from "./components/SinglePhoto";
import { getSingleObject, listObjects } from "../utils/index.js";


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
     let results = [];
     for(let i = 0; i < 10; i ++) {
       results.push(data[i].Key)
     }
     return results;
    })
    .then((keysArr) => {
      console.log(keysArr);
      return keysArr.map((key) => {
        return getSingleObject(key);
      });
    })
    .then((photos)=>{
      Promise.all(photos)
      .then((b64arr)=>{
        this.photos = b64arr.map((b64str) => {
          return  "data:image;base64," + b64str;
        })
        })
    });
  },
  methods: {
    changeView: function(newValue) {
      this.currentView = newValue;
    },
    updatePhotosAfterUpload: function() {
      listObjects()
      .then((data) => {
        let results = [];
        for(let i = 0; i < 10; i ++) {
          results.push(data[i].Key)
        }
        return results;
      })
      .then((keysArr) => {
      
      return keysArr.map((key)=> {
        return getSingleObject(key);
      })
      .then((photos) => {
        Promise.all(photos).then((b64arr)=>{
        this.photos = b64arr.map((b64str) => {
          return  "data:image;base64," + b64str;
        })
        })
      });
    });
    },
  }
};
</script>

<style>
#app {
  text-align: center;
}
</style>
