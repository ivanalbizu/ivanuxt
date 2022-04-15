<template>
  <section class="content">
    <header class="post-head">
      <h1 class="page-title">{{ article.title }}</h1>
      <blockquote>{{ article.description }}</blockquote>
      <blog-thumb v-if="article.cover_image" :article="article"></blog-thumb>
      <div class="blog__details">
        <blog-date :date="article.ctime"></blog-date>
        <blog-tags :tags="article.tags"></blog-tags>
      </div>
    </header>
    <article>
      <nuxt-content :document="article" />
    </article>
    <footer class>
      <nuxt-link to="/blog/" class>&larr; Volver al blog</nuxt-link>
    </footer>
  </section>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const article = await $content('blog', params.slug).fetch()
    return { article }
  },
  head() {
    return {
      title: `${this.article.title} | Maquetador Web`,
      meta: [
        {
          hid: "description",
          name: "description",
          content: this.article.description
        }
      ]
    };
  }
}
</script>
