<template>
  <div class="root">
    <h1>{{ post.fields.title }}</h1>
  </div>
</template>

<script>
import Vue from 'vue'
import createClient from '~/plugins/contentful'

export default Vue.extend({
  head() {
    console.log(this.post.fields.thumbnail.fields.file.url)
    return {
      title: this.post.fields.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.post.fields.description
        },
        {
          hid: 'og:image',
          name: 'og:image',
          content: this.post.fields.thumbnail.fields.file.url
        }
      ]
    }
  },
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
