<template>
  <main class="main">
    <article-list :articles="articles" :title="'Entradas'"></article-list>
    <blog-aside-tags></blog-aside-tags>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content('blog', params.slug)
      .only(['title', 'description', 'cover_image', 'slug', 'tags', 'ctime'])
      .sortBy('ctime', 'desc')
      .fetch()

    return { articles }
  },
  head() {
    return {
      title: 'Publicaciones sobre html, js, css',
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Publicaciones sobre html, js, css, sass. Ejemplos de modales, slides y mucho más"
        }
      ]
    };
  }
}
</script>

<style lang="scss" scope>
.nuxt-content {
  p,
  figure,
  .nuxt-content-highlight {
    margin-bottom: 2rem;
  }
}
</style>
