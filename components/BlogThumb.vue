<template>
  <figure class="blog__img">
    <img
      :src="require(`~/assets/images/blog/${article.cover_image}`)"
      :alt="article.alt_image"
      loading="lazy"
      width="1482"
      height="404"
    />
  </figure>
</template>

<script>
export default {
  props: {
    article: {
      type: Object,
      required: true
    }
  }
}
</script>