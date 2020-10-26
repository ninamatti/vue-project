<template>
<div>
  <h1
      v-on:click="$emit('change-view', 'AllPhotos')" >
      I am a navbar emitter! HI</h1>
  <upload v-on:file-uploaded="$emit('on-upload')"  />
</div>
</template>

<script>
import Upload from "./Upload.vue"
export default {
  name: "Navbar",
  components: {
    upload: Upload,
  }
};
</script>

<style></style>
