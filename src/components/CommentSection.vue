<template>
Komentarze
    <div class="comment-section">
      <div class="addComment">
        <input type="text" v-model="comment">
        <button @click="addComment()">Add</button>
      </div>
      <div class="comment" v-for="comment in commentList" :key="comment">
        <div class="avatar">
          <img src="https://via.placeholder.com/50">
        </div>
        <div class="about">
          <div class="creator">
            {{comment.addedBy}}, {{comment.time}}
          </div>
          <div class="content">
            <span v-if="!comment.editMode">{{comment.content}}</span>
            <div v-else><input type="text" v-model="editedComment">
              <button @click="saveEditComment(comment.content !== editedComment)">Zapisz</button> <button @click="cancelEdit()">Anuluj</button>
            </div>
          </div>
          <div class="actions">
            <span style="text-decoration:underline" @click="editComment(comment.id)">Edytuj</span>
            <span style="text-decoration:underline" @click="deleteComment(comment.id)">Usuń</span>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  name: 'requirements',
   data () {
    return {
      comment:'',
      commentList: [],
      commentId: 0,
      editedComment: ''
    }
  },
  methods: {
    addComment() {
      if(this.comment.length === 0) return
      this.commentList.push({
          id: this.commentId,
          content: this.comment,
          status: false,
          addedBy: 'Stanisław Kozioł',
          time: moment().locale('pl').format('DD-MM-YYYY, HH:mm:ss '),
          editMode: false
        })
      this.comment = ''
      this.commentId++
    },
    deleteComment(id) {
      const commenttoDelete = this.commentList.find(c => c.id == id)
      this.commentList.splice(this.commentList.indexOf(commenttoDelete), 1)
    },
    editComment(id) {
      const commenttoEdit = this.commentList.find(c => c.id == id)
      this.editedComment = commenttoEdit.content
      commenttoEdit.editMode = true
    },
    saveEditComment(isChange) {
      if(isChange) {
        const editingComment = this.commentList.find(c => c.editMode == true)
        editingComment.content = this.editedComment;
        editingComment.editMode = false
      }
    },
    cancelEdit(){
      const editingComment = this.commentList.find(c => c.editMode == true)
      editingComment.editMode = false
    }
  }
}
</script>

<style lang="scss" scoped>
.comment-section{
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
    .avatar{
      border-radius: 50%;
      overflow: hidden;
    }

    .about{
      display:flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: center;
    }
  }
  

  .addComment{
  display:flex;
  } 
}
</style>