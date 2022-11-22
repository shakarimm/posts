<template>
  <div
      class="wrapper"
      :class="{wrapperActive: isActive}"
  >
    <div class="title">Shakarim's Blog</div>
    <div class="posts">
      <post-list
          :posts="posts"
          @remove="removePost"
          v-if="!isPostsLoading"
      />
      <div v-else>Loading...</div>
    </div>
    <div class="addBtn-wrapper">
      <div
          class="btn addBtn"
          @click="openModal"
      >
        Add
      </div>
    </div>
  </div>
  <post-form
      @create="createPost"
      :class="{formActive: isActive}"
      @close="openModal"
  />
</template>

<script>
import PostList from "@/components/PostList";
import PostForm from "@/components/PostForm";
import axios from 'axios'

  export default {
    components: {
      PostForm, PostList
    },
    data() {
      return {
        posts: [],
        isActive: false,
        isPostsLoading: false,
      }
    },
    methods: {
      openModal() {
        this.isActive = !this.isActive
      },
      createPost(post) {
        this.posts.push(post)
        this.isActive = !this.isActive
      },
      removePost(post) {
        this.posts = this.posts.filter(p => p.id !== post.id)
      },
      async fetchPosts() {
        try {
          this.isPostsLoading = true;
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
          this.posts = response.data
          console.log(this.posts)
        } catch (e) {
          alert('Error')
        } finally {
          this.isPostsLoading = false;
        }
      }
    },
    mounted() {
      this.fetchPosts();
    }
  }
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app{
  font-family: 'Nunito', sans-serif;
  height: 100vh;
  padding: 4em 16em;
  font-size: 18px;
}
.wrapperActive{
  opacity: 0.5;
}
/*.posts{*/
/*  display: flex;*/
/*  justify-content: space-between;*/
/*  flex-wrap: wrap;*/
/*  margin-top: -20px;*/
/*}*/
.wrapper{
  position: relative;
  z-index: 100;
}
.title{
  width: 100%;
  font-size: 32px;
  line-height: 46px;
  margin-bottom: 30px;
  font-weight: 700;
  text-align: center;
}
.btn{
  background: #7FFF00;
  padding: 8px 16px;
  border: none;
  border-radius: 8px;
  text-transform: uppercase;
  cursor: pointer;
  font-weight: 700;
  transition: all .4s;
  margin-top: 20px;
}
.btn:hover{
  opacity: 0.5;
}
.addBtn-wrapper{
  display: flex;
  justify-content: flex-end;
}
</style>