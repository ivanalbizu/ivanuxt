<template>
  <section v-if="articles" class="content-articles">
    <header class="header-blog">
      <h1 class="page-title">{{ title }}</h1>
    </header>
    <article v-for="article in articles" :key="article.title" class="blog">
      <h2><nuxt-link :to="`${path}/${article.slug}`" class="post-title">{{ article.title }}</nuxt-link></h2>
      <!-- TO-DO: props article to blog-thumb -->
      <blog-thumb v-if="article.cover_image" :article="article"></blog-thumb>
      <div class="blog__details">
        <blog-date :date="article.ctime"></blog-date>
        <blog-tags :tags="article.tags"></blog-tags>
      </div>
      <p class="blog__excerpt">{{ article.description }}</p>
      <nuxt-link :to="`/blog/${article.slug}`">Leer m&aacute;s <span class="visually-hidden">sobre {{ article.title }}</span> &rarr;</nuxt-link>
    </article>
  </section>
</template>

<script>
import BlogThumb from './BlogThumb.vue'
export default {
  components: { BlogThumb },
  props: {
    title: {
      type: String,
      required: true
    },
    articles: {
      type: Array,
      required: true
    },
    path: {
      type: String,
      default: '/blog'
    }
  }
}
</script>

<style lang="scss">
.blog {
  margin-bottom: 5rem;
  &__img {
    margin-bottom: .5rem;
  }
  &__excerpt {
    margin-bottom: 1rem;
  }
  &__details {
    display: grid;
    gap: 0 1.5rem;
    justify-content: space-between;
    margin-bottom: 1.5rem;
  }
  @media (min-width: 575px) {
    &__details {
      grid-auto-flow: column;
    }

  }
}
</style>
