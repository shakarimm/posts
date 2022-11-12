<template>
  <div class="post">
    <div class="post-title">{{ post.title }}</div>
    <div class="post-body">{{ post.body }}</div>
    <button class="btn" @click="$emit('remove', post)">Удалить</button>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    }
  }
}
</script>

<style scoped>
.post{
  text-align: center;
  background: #f5f5f5;
  padding: 20px;
  border-radius: 8px;
  width: 30%;
  margin-top: 20px;
}
.post-body{
  margin-top: 20px;
}
.post-title{
  font-weight: 700;
  font-size: 20px;
}
</style>