<template>
    <div class="comments-container">
      <h2>Commentaires</h2>
      <ul class="comments-list">
        <li v-for="(item, index) in comments" :key="index" >
          <div class="comment">
            <div class="author-photo">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
              </svg>
            </div>
            <div class="comment-details">
                <input class="comment-input" ref="authorInput" type="text" v-model="item.author" placeholder="Author" />
                <textarea class="comment-input" ref="contentInput" v-model="item.content" placeholder="Comment">
                </textarea>
            </div>
            <div class="actions">
              <div class="delete" @click="onDelete(index)">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                </svg>
              </div>
              <div class="edit" @click="onEdit(index)">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z" />
                </svg>
              </div>
            </div>
          </div>
        </li>
      </ul>
      <div class="add-comment" @click="addComment()">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
        </svg>
      </div>
    </div>
</template>

<script>
export default {
  name: 'Comment',
  props: ['comments'],
  data () {
    return {
      newComment: {}
    }
  },
  methods: {
    onDelete (index) {
      // Appelle du fonction onDeletedComment (in the Parent Component - Container)
      this.$emit('deleted', index)
    },
    onEdit (index) {
      // Set Focus au commentaire à modifier
      this.$refs.contentInput[index].focus()
      console.log('edited')
    },
    addComment () {
      this.newComment.author = ''
      this.newComment.content = ''
      // Add item to comments
      this.comments.push(this.newComment)
      // Set Focus To the last authorInput
      this.$refs.authorInput[this.comments.length - 1].focus()
      // Vue.nextTick(function () { this.$refs.authorInput[this.comments.length - 1].focus() })
    }
  }
}
</script>

<style>
.comments-container {
  height: 100%;
  padding: 10px 20px 10px 10px;
  overflow-y: auto;
}

.comments-container h2 {
  font-size: 22px;
  font-weight: 600;
  margin-bottom: 15px;
  text-align: center;
}

.comments-list {
  list-style-type: none;
  padding: 0;
}

.comments-list li {
  margin: 10px 0;
  background: rgba(219, 234, 254, 0.6);
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  border-radius: 20px;
  padding: 10px 20px 10px 10px;
  position: relative;
  font-size: 14px;
  height: 90px;
}

.comment {
  display: flex;
  align-items: center;
}

.author-photo {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  border: 1px solid #fff;
  margin-right: 10px;
}

.author-photo svg {
  width: 50%;
  color: #fff;
}

.comment-details {
  width: 80%;
}

.comment-details h5 {
  font-size: 15px;
  font-weight: bold;
  margin: 0 0 6px;
}

.comment-details p {
  font-size: 14px;
  font-style: italic;
  margin: 0;
}

.comment-input {
  width: 85%;
  background: transparent;
  border: none;
  resize: none;
  padding: 1px;
}

.comment-input:focus {
  outline: 0;
  border: 2px dotted #93C5FD;
}
.actions {
  height: 100%;
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  z-index: 10;
  right: -12px;
  top: 0;
}

.edit, .delete {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  width: 25px;
  height: 25px;
  background: linear-gradient(90deg,
                rgba(78,169,228,1) 0%,
                rgba(102,193,236,0.7959558823529411) 88%,
                rgba(151,205,215,1) 100%);
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  border-radius: 50%;
  opacity: 0.7;
  transition: opacity 0.3s ease-in-out;
}

.edit:hover, .delete:hover {
  opacity: 1;
}

.edit svg, .delete svg {
  width: 15px;
  height: 15px;
  color: #fff;
}

.delete {
  margin-bottom: 5px
}

.add-comment {
  margin: 20px auto;
  width: 80px;
  height: 80px;
  cursor: pointer;
  border-radius: 50%;
  border: 1px solid #fff;
  transition: all 0.3s ease-in-out;
}

.add-comment:hover {
  transform: scale3d(1.1,1.1,1.1);
}

.add-comment svg {
  width: 100%;
  height: 100%;
  color: #fff;
}

@media(max-width: 767px) {
  .comments-container {
    padding: 20px;
  }
}
</style>
