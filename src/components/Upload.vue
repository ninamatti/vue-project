<template>
<div >
  <h3>Upload to space</h3>
  <input v-on:change="fileUpdater" type="file" /> 
  <button v-on:click="saveFiletoAWS">Upload</button>
</div>
</template>

<script>
import { saveObject, listObjects } from "../../utils/index.js";
// get file input✅

// save file to s3 bucket ✅

// update photos array because we added our own photo
export default {
  name: "Upload",
  data: () => ({
    file: "",
  }),
  methods: {
    saveFiletoAWS: function() {
      saveObject(this.file)
      .then(()=>{
       this.$emit('file-uploaded');
    });
    },
    fileUpdater: function(e){
      this.file = e.target.files[0];
    }
  }
};
</script>

<style></style>
