<template>
  <div>
    <h3>ALL PHOTOS</h3>
    <template v-for="photo in photos">
      <img v-bind:key="photo" :src="photo">

    </template>
  </div>
</template>

<script>
// console.log('I am in allphotos! ', this.photos)
// array of b64 with srcs. loop over and show on screen

export default {
  name: "AllPhotos",
  props: ['photos'],
};
</script>

<style></style>
