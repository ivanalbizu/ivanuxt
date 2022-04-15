<template>
  <ul class="tags">
    <li v-if="tagAll">
      <nuxt-link :to="'/blog'">Todas</nuxt-link>
    </li>
    <li v-for="(tag, index) in tags" :key="index">
      <nuxt-link :to="`/blog/tag/${tag}`"><span class="visually-hidden">Ver entradas con la categoría </span>{{ tag }}</nuxt-link>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    tags: {
      type: Array,
      required: true
    },
    tagAll: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="scss" scoped>
.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  li {
    display: flex;
    align-items: center;
    font-size: 1.3rem;
    font-style: italic;
  }
}
.aside-tags {
  .tags {
    a {
      color: var(--color-bg);
      background-color: var(--primary);
      padding: .1rem .9rem;
      transition: all .2s linear;
      &.nuxt-link-exact-active,
      &:hover,
      &:focus {
        background-color: var(--link-hover);
        transition: all .2s linear;
      }
      &.nuxt-link-exact-active {
        cursor: default;
      }
    }
  }
}
</style>
