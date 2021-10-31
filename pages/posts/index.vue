<template>
  <div class="root">
    <button @click="handleClick">click here</button>
    <div v-for="(post, index) in posts" :key="index">
      <!-- <nuxt-link :to="{name: 'sample', params: {slug: item.slug}}"> -->
      <nuxt-link :to="`/posts/${post.fields.slug}`">
        <p>{{ post.fields.title }}</p>
      </nuxt-link>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import createClient from '~/plugins/contentful'

export default Vue.extend({
  async asyncData() {
    const contentful = createClient()
    const entries = await contentful
      .getEntries({
        content_type: 'test',
      })
      .catch(console.error)

    return {
      posts: entries.items
    }
  },

  methods: {
    handleClick() {
      console.log(this.posts)
    }
  }
})
</script>
