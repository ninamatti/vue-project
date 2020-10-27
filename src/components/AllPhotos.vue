<template>
  <div>
    <h3>ALL PHOTOS</h3>
    <template v-for="photo in photos">
      <img
        class="photo"
        v-bind:key="photo"
        :src="photo"
        v-on:click="selectPhoto(photo)"
      />
    </template>
  </div>
</template>

<script>
export default {
  name: "AllPhotos",
  props: ["photos"],
  methods: {
    selectPhoto: function(photo) {
      this.$emit("file-selected", photo);
    }
  }
};
</script>

<style>
.photo {
  width: 300px;
  height: 300px;
  border: 4px solid #35495e;
  margin: 5px;
}
</style>
