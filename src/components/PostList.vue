<template>
    <div class="post-list">
      <article v-for="post in posts" :key="post.id" class="card mb-3 shadow-sm">
        <div class="card-body">
          <h4>{{ post.title }}</h4>
          <div class="row my-3 align-items-center">
            <div v-if="post.image" class="col-3">
              <img :src="post.image" :alt="post.title" class="rounded-lg w-100">
            </div>
            <p :class="{'col-9': post.image}" >{{post.content}}</p>
          </div>
          <span >{{post.createAt}}</span>
        </div>
      </article>
    </div>
  </template>

<script lang="ts">
import { PostProps } from '@/testData'
import { defineComponent, PropType } from 'vue'
export default defineComponent({
  props: {
    list: {
      required: true,
      type: Array as PropType<PostProps[]>
    }
  },
  setup (props) {
    // eslint-disable-next-line vue/no-setup-props-destructure
    const posts = props.list
    return {
      posts
    }
  }
})
</script>

  <style scoped>
  .post-list h4 a {
    text-decoration: none;
    color:#1a1a1a;
  }
  .post-list h4 a:hover {
    color:#0d6efd;
  }
  </style>
