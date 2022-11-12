<template>
  <form
      @submit.prevent
      class="form"
  >
    <div
        class="close"
        @click="closeModal"
    >✖</div>
    <input
        class="input"
        type="text"
        placeholder="Title"
        v-model="post.title"
    >
    <input
        class="input"
        type="text"
        placeholder="Content"
        v-model="post.body"
    >
    <button
        class="btn"
        @click="createPost"
    >Create
    </button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: '',
        body: '',
      },
      isActive: false,
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: '',
      }
    },
    closeModal() {
      this.$emit('close')
    }
  }
}
</script>

<style scoped>
.form{
  width: 500px;
  padding: 40px 20px;
  background: #f5f5f5;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translateY(-50%) translateX(-50%);
  opacity: 0;
}
.formActive{
  opacity: 1;
}
.input{
  width: 100%;
  padding: 10px 15px;
  margin-top: 20px;
  border-radius: 8px;
  border: none;
}
.close{
  display: flex;
  justify-content: flex-end;
  cursor: pointer;
}
</style>