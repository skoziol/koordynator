<template>
  Załączniki
    <div class="file-section">
      <div class="comment" v-for="comment in fileList" :key="comment">
        <img src="@/assets/doc.png" width="80" height="60" style="margin:0 10px">
        <div class="about">
          <span class="name">
            sample{{comment.id}}.doc
          </span>
          <div class="creator">
           Dodano: {{comment.time}},
            <span style="text-decoration:underline" @click="editComment(comment.id)">Edytuj</span>
            <span style="text-decoration:underline" @click="deleteComment(comment.id)">Usuń</span>
          </div>
          <span class="who">{{comment.addedBy}}</span>
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
      fileID: 0,
      editedComment: ''
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
      this.comment = ''
      this.fileID++
    },
    deleteComment(id) {
      const commenttoDelete = this.fileList.find(c => c.id == id)
      this.fileList.splice(this.fileList.indexOf(commenttoDelete), 1)
    },
    editComment() {
      console.log('edit')
    },
    saveEditComment(isChange) {
      if(isChange) {
        const editingComment = this.fileList.find(c => c.editMode == true)
        editingComment.content = this.editedComment;
        editingComment.editMode = false
      }
    },
    cancelEdit(){
      const editingComment = this.fileList.find(c => c.editMode == true)
      editingComment.editMode = false
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

  .comment{
    display:flex;
    align-items: center;
    justify-content: flex-start;
    height: min-content;
    width: 100%;
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