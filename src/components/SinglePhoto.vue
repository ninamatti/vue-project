<template>

 <img v-bind:src="selectedPhoto"/>
</template>

<script>
export default {
  name: "SinglePhoto", 
  props: ['selectedPhoto'],
};

</script>

<style></style>
