<template>
<div>
  <h1 v-on:click="$emit('change-view', 'AllPhotos')" >I am a navbar emitter! HI</h1>
</div>
</template>

<script>
export default {
  name: "Navbar",
};
</script>

<style></style>
