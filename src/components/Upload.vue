<template>
<div >
  <div>
    <input class="button" v-on:change="fileUpdater" type="file" /> 
  <div>    
  </div>
    <button class="button" v-on:click="saveFiletoAWS">Upload</button> 
  </div>
  
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

<style>

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
