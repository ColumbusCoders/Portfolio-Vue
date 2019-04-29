<template>
  <div>
     <h3>Upload Image </h3>
     <input type="text"  v-model="userName" id="firstName">
     <input type="file" @change="onFileChanged">
     <button @click="onUpload">Upload!</button>
  </div>
</template>

<script>
import axios from 'axios'

export default 

{
      data() {
        return {
          selectedFile: null,
          userName : ''
        }
      },
      methods: {
        onFileChanged (event) {
          this.selectedFile = event.target.files[0]

        },
        onUpload() {
          let config = {
                          headers: { 'Content-Type': 'multipart/form-data' }
                        };
         let params = new URLSearchParams();
         params.append('fileName', this.selectedFile);
         params.append('userName', this.userName);

              axios.post('http://localhost:8080/imgStore/' + this.userName, params, config)
                  .then((response) => {
                      console.log(response.data);
              });
          // upload file, get it from this.selectedFile
        }

      }
}
</script>