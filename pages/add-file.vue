<template>
  <div style="max-width: 1200px; margin-left: auto; margin-right: auto">
    <div class="block" style="width: auto">
      <h1 class="title">Add file to resource</h1>
      <div class="description">
        Resource ID: <input id="id" class="input-box" type="text" placeholder="Reosurce ID"/><br>
        Description: <input id="description" class="input-box" type="text" placeholder="Description"/><br>
        Versions: <input id="versions" class="input-box" type="text" placeholder="Versions"/><br>
        Version: <input id="version" class="input-box" type="text" placeholder="Version"/><br>
        File: <input id="file" class="input-box" type="file" placeholder="File"/><br>
      </div>
      <p class="description">Add a new resource to be archived.</p>
      <button v-on:click="addResource">Add</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'add',
  methods: {
    addResource: function() {
      const config = {
        headers: {
          //Accept: "application/json",
          'Content-Type': 'multipart/form-data'
        }
      };

      const id = document.getElementById('id').value
      const description = document.getElementById('description').value;
      const version = document.getElementById('version').value;
      const versions = document.getElementById('versions').value;
      const file = document.getElementById('file').files[0];
      const data = {
        id: id,
        description: description,
        version: version,
        versions: [versions]
      }

      let formData = new FormData();
      formData.append('file', file);
      formData.append('data', JSON.stringify(data));

      axios.post('http://localhost:8080/file/upload', formData, config).then(function(response) {
        console.log(response);
      }).catch(function(error) {
        console.log(error);
      });
    }
  }
}
</script>

<style scoped>
.block {
  background: rgba(51, 50, 50, 0.5);
  border-radius: 6px;
  padding: 10px;
  margin: 8px 0;
}

.title {
  font-size: 20px;
  text-decoration-thickness: auto;
  color: #0ca8a8;
}

.description {
  color: white;
  text-decoration-thickness: 1px;
}

.input-box {
  margin: 5px 0;
  color: black;
  padding: 0 5px;
}
</style>
