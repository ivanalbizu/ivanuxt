<template>
  <main class="main">
    <article-list :articles="articles" :title="`Entradas de categoría: ${tag}`" :path="'..'"></article-list>
    <blog-aside-tags></blog-aside-tags>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content('blog')
      .where({
        tags: { $contains: params.slug }
      })
      .sortBy('ctime', 'desc')
      .fetch()
    return {
      articles,
      tag: params.slug
    }
  },
  head() {
    return {
      title: `Entradas de categoría: ${this.tag}`,
      meta: [
        {
          hid: "description",
          name: "description",
          content: `Maquetador Web. Publicaciones de Blog bajo la categoría: ${this.tag}`
        }
      ]
    };
  }
}
</script>
