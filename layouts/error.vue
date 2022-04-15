<template>
  <main class="main main--error">
    <h1 v-if="error.statusCode === 404">Page not found</h1>
    <h1 v-else>An error occurred</h1>
    <NuxtLink to="/">Home page</NuxtLink>
  </main>
</template>

<script>
export default {
  props: {
    error: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.main {
  &--error {
    text-align: center;
    min-height: 20rem;
  }
}
</style>
