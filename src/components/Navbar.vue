<template>
<div class="navbar">
  <h1 class="button"
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

<style>
.navbar {
  background-color: white;
  border-top: 10px solid #35495e;
  border-bottom: 10px solid #35495e;
  width: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;}



.button {
  padding: 15px 30px;
  font-size: 20px;
  font-weight: 900; 
  color: #fff;
  background-color:  #41b883;
  border: 2px solid  #41b883;
  cursor: pointer;
  width: max-content;
  transition: 0.25s ease;
  margin: 5px;
}

button:hover {
    border-color: #41b883;
    background-color:  #35495e;
}

</style>
