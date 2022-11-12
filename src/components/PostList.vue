<template>
  <div
      v-if="posts.length > 0"
      style="display: flex; justify-content: space-between; flex-wrap: wrap"
  >
    <post-item
        v-for="post in posts"
        :post="post"
        :key="post.id"
        @remove="$emit('remove', post)"
    />
  </div>
  <div v-else>
    <h2 style="color: red; text-align: center">Post list is empty</h2>
  </div>
</template>

<script>
import PostItem from "@/components/PostItem";
export default {
  components: {
    PostItem
  },
  props: {
    posts: {
      type: Array,
      required: true,
    }
  }
}
</script>

<style scoped>

</style>