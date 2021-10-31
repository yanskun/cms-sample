<template>
  <div class="root">
    <h1>{{ post.fields.title }}</h1>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import createClient from '~/plugins/contentful'

export default Vue.extend({
  async asyncData({ params }) {
    const contentful = createClient()
    const entries = await contentful
      .getEntries({
        content_type: 'test',
        'fields.slug': params.slug
      })
      .catch(console.error)
    return {
      post: entries.items[0]
    }
  }
})
</script>
