<template>
<div>
  <h1
      v-on:click="$emit('change-view', 'AllPhotos')" >
     HOME</h1>
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
