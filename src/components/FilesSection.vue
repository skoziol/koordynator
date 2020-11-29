<template>
  Załączniki
    <div class="file-section">
      <div class="file" v-for="file in fileList" :key="file">
        <img src="@/assets/doc.png" width="80" height="60" style="margin:0 10px">
        <div class="about">
          <span class="name">
            sample{{file.id}}.doc
          </span>
          <div class="creator">
           Dodano: {{file.time}},
            <span style="text-decoration:underline" @click="editFile(file.id)">Edytuj</span>
            <span style="text-decoration:underline" @click="deleteFile(file.id)">Usuń</span>
          </div>
          <span class="who">{{file.addedBy}}</span>
        </div>
      </div>
      <div class="addFile">
        <button @click="addFile()">Add</button>
      </div>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  name: 'requirements',
   data () {
    return {
      fileList: [],
      fileID: 0
    }
  },
  methods: {
    addFile() {
      this.fileList.push({
          id: this.fileID,
          status: false,
          addedBy: 'Stanisław Kozioł',
          time: moment().locale('pl').format('DD-MM-YYYY, HH:mm:ss '),
          editMode: false
        })
      this.fileID++
    },
    deleteFile(id) {
      const FiletoDelete = this.fileList.find(c => c.id == id)
      this.fileList.splice(this.fileList.indexOf(FiletoDelete), 1)
    },
    editFile() {
      console.log('edit')
    }
  }
}
</script>

<style lang="scss" scoped>
.file-section{
  flex-grow:1;
  display:flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;

  .file{
    display:flex;
    align-items: center;
    justify-content: flex-start;
    height: min-content;
    width: 100%;
    margin: 10px 0;

    .about{
      display:flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: center;
    }
  }
  

  .addFile{
  display:flex;
  } 
}
</style>