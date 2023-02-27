<template>
  <PostForm :post="post" :submitForm="createPost" />
</template>

<script>
import PostForm from '../components/PostForm.vue'
import { reactive } from 'vue'
import { useRouter } from 'vue-router'
export default {
  components: {
    PostForm,
  },
  setup() {
    const API_URL = 'https://crud-vue-backend.vercel.app/posts'
    const router = useRouter()

    const headers = { 
      "Content-Type": "application/json",
      "Access-Control-Allow-Origin": "*",
      "Access-Control-Allow-Credentials": "true",
      "Access-Control-Max-Age": "1800",
      "Access-Control-Allow-Headers": "Content-Type",
      "Access-Control-Allow-Methods": "PUT, POST, GET, DELETE, PATCH, OPTIONS"
    };

    const post = reactive({
      title: '',
      content: '',
      creator: '',
    })

    async function createPost() {
      try {
        const response = await fetch(API_URL, {
          method: 'POST',
          headers,
          body: JSON.stringify({
            title: post.title,
            content: post.content,
            creator: post.creator,
          }),
        })
        const json = await response.json()
        router.push({
          name: 'Home',
        })
      } catch (error) {
        console.log(error)
      }
    }
    return {
      post,
      createPost,
    }
  },
}
</script>

<style></style>
