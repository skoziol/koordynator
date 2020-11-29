<template>
  <h3>Komentarze</h3>
    <div class="comment-section">
      <div class="addComment" :class="{isFocused: gondor, notFocused: !gondor}"> 
        <button v-show="!gondor" @click="gondor = true">Dodaj Komentarz</button>
        <textarea v-show="gondor" @show="focus" rows="4" v-model="comment"></textarea>
        <div class="row">
          <button @click="addComment()" :class="{active: comment.length > 0}" v-show="gondor">Dodaj</button>
          <button @click="gondor = false; comment='';" v-show="gondor">Anuluj</button>
        </div>
      </div>
      <div class="comment" v-for="comment in commentList" :key="comment">
        <div class="avatar">
          <img src="https://via.placeholder.com/30">
        </div>
        <div class="about">
          <div class="creator">
            <span style="font-size: 17px; font-weight: 500;">{{comment.addedBy}}</span>,
            <span style="font-size: 15px; color:gray;">{{comment.time}}</span>
          </div>
          <div class="content">
            <span v-if="!comment.editMode">{{comment.content}}</span>
            <div v-else class="editComment">
              <textarea row="3" cols="20" type="text" v-model="editedComment"/>
              <div style="display:flex" >
                <button @click="saveEditComment(comment.content !== editedComment)" :class="{active: editedComment !== comment.content}">Zapisz</button>
                <button style="margin-left: 10px;" @click="cancelEdit()">Anuluj</button>
              </div>
            </div>
          </div>
          <div class="actions"  v-if="!comment.editMode">
            <span style="text-decoration:underline;" @click="editComment(comment.id)">Edytuj</span>
            <span style="text-decoration:underline; margin-left: 10px;" @click="deleteComment(comment.id)">Usuń</span>
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
      editedComment: '',
      gondor: false
    }
  },
  methods: {
    addComment() {
      if(this.comment.length === 0) return
      this.commentList.unshift({
          id: this.commentId,
          content: this.comment,
          status: false,
          addedBy: 'Stanisław Kozioł',
          time: moment().locale('pl').format('DD-MM-YYYY, HH:mm'),
          editMode: false
        })
      this.comment = ''
      this.commentId++
      this.gondor = false
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
  margin: 0 20px;
  display:flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;

  .comment{
    display:flex;
    align-items: flex-start;
    justify-content: flex-start;
    height: min-content;
    width: 90%;
    margin: 5px 0;

    .avatar{
      align-items: flex-start;
      border-radius: 50%;
      overflow: hidden;
      height: 30px;
      width: 30px;
      margin-top: 5px;
      margin-right: 5px;
    }

    .about{
      display:flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: center;

      button{
        align-items: center;
        justify-content: center;
        font-size: 17px;
        font-weight: 500;
        height: 30px;
        width: 60px;
        transition: 0.25s ease;
        margin-top: 10px;
        &.active{
          background: #2196F3;
          color: white;
        }
      }
    }

    .content{
      display: flex;;
      span{
        background:  #eeeeee;
        border-radius: 3px;
        margin: 5px 0 ;
        padding: 5px;
        
        width: min-content;
        height: min-content;
      }
    }
  }
  
  .addComment{
    display:flex;
    align-self: flex-start;
    flex-direction: column;
    position: relative;
    margin: 10px 0 ;

    .row{
      display:flex;

      button{
        &+button{
          margin-left:10px;
        }
      }
    }

    &.isFocused{
      button{
        align-items: center;
        justify-content: center;
        font-size: 17px;
        font-weight: 500;
        height: 30px;
        width: 60px;
        transition: 0.25s ease;
        margin-top: 10px;
        &.active{
          background: #2196F3;
          color: white;
        }
      }
    } 

    &.notFocused{
      button{
        display: flex;
        align-items: center;
        justify-content: center;
        border: none;
        background: lightgray;
        font-size: 16px;
        color: black;
        height: 30px;
        width: 150px;
        
      }
    }
  } 
}
</style>