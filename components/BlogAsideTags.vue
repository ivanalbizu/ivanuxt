<template>
  <aside class="aside">
    <div class="aside-tags">
      <p>Categorías</p>
      <blog-tags :tags="tags" :tag-all="true"></blog-tags>
    </div>
  </aside>
</template>

<script>
export default {
  data() {
    return {
      tags: ['html', 'css', 'javascript', 'webgl', 'nodejs', 'vue', 'pug', 'java', 'android', 'php', 'wordpress']
    }
  }
}
</script>

<style lang="scss" scoped>
.aside-tags {
  position: sticky;
  top: 20px;
  margin-bottom: 3rem;
}
</style>