<template>
  <div id="app">
    
    <h1>{{ title }}<img class="logo" alt="Vue logo" src="./assets/logo.png" /></h1>
    
    <navbar  v-on:change-view="changeView"
             v-on:on-upload="updatePhotosAfterUpload"/>
    <h2 v-if="loading === true" class="loader"> 🚴🏽‍♀️🚴🏽‍♀️🚴🏽‍♀️🚴🏽‍♀️🚴🏽‍♀️ LOADING 🚴🏽‍♀️🚴🏽‍♀️🚴🏽‍♀️🚴🏽‍♀️🚴🏽‍♀️</h2>
    <allphotos v-if="currentView === 'AllPhotos'" 
               v-bind:photos="photos"
               v-on:file-selected="setSinglePhoto"/>
    <singlephoto v-else v-bind:selectedPhoto="selectedPhoto"/>
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
    currentView: "AllPhotos",
    photos: [],
    selectedPhoto: "image",
    loading: true,
  }),
  created() {
    listObjects()
    .then((data) => {
     let results = [];
     for(let i = 0; i < 10; i ++) {
       results.push(data[i].Key)
     }
     return results;
    })
    .then((keysArr) => {
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
        this.loading = false;
        })
    });
  },
  methods: {
    changeView: function(newValue) {
      this.currentView = newValue;
    },
    setSinglePhoto: function(e) {
      this.selectedPhoto = e;
      this.currentView = "SinglePhoto";
    },
    updatePhotosAfterUpload: function() 
    {
      listObjects()
      .then((data) => {
        let results = [];
        for(let i = 0; i < 10; i ++) {
          results.push(data[i].Key)
        }
        return results;
      })
      .then((keysArr) => {
        console.log("KEYS ARRR UPLOAD", keysArr);
        return keysArr.map((key)=> {
          return getSingleObject(key);
      })})
      .then((photos) => {
        Promise.all(photos)

        .then((b64arr) =>{
          this.photos = b64arr.map((b64str) => {
          return  "data:image;base64," + b64str;
        })
      })
      });

    },
  }
};
</script>

<style>

@font-face {
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: local('Source Sans Pro Regular'), local('SourceSansPro-Regular'), url(https://fonts.gstatic.com/s/sourcesanspro/v14/6xK3dSBYKcSV-LCoeQqfX1RYOo3qOK7lujVj9w.woff2) format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
}

#app {
  font-family: 'Source Sans Pro';
}

h1 {
  vertical-align:middle;
}

.logo {
  width: 35px;
  height: auto;
  margin-left: 10px;
  vertical-align: middle; 
}

@keyframes myanimation
{
    from {
        margin-left: 100%;
        width: 300%;
    }
    to {
        margin-left: 0%;
        width: 100%;
    }
}


.loader {
  color:  #41b883;
  animation-name: myanimation;
  animation-duration: 2s;
  animation-iteration-count: infinite;
}
</style>
