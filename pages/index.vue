<template>
  <div>
    <site-hero></site-hero>
    <main class="main">
      <article-list :articles="articles" :title="'Últimas publicaciones'"></article-list>
      <blog-aside-tags></blog-aside-tags>
    </main>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content('blog', params.slug)
      .only(['title', 'description', 'cover_image', 'slug', 'tags', 'ctime', 'alt_image'])
      .sortBy('ctime', 'desc')
      .limit(3)
      .fetch()

    return { articles }
  },
}
</script>
