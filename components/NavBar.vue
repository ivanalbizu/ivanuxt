import NavBar from '~/components/NavBar';
<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <nuxt-link class="navbar__title" to="/">ivan albizu</nuxt-link>
    <div class="navbar__menu">
      <nuxt-link class="button" to="/curriculum/">Currículum</nuxt-link>
      <nuxt-link class="button" to="/blog/">Blog</nuxt-link>
      <ColorModePicker />
    </div>
  </nav>
</template>

<script>
export default {
  name: "Navbar"
};
</script>

<style lang="scss">
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  min-height: 5rem;
  margin-bottom: 4rem;
  font-size: clamp(1.8rem, 3vw, 3rem);
  &__menu {
    display: grid;
    grid-auto-flow: column;
    align-items: center;
    gap: 1rem;
    gap: clamp(1rem, 2vw, 3rem);
    a {
      border-bottom: 3px solid transparent;
    }
    .nuxt-link-active {
      border-bottom: 3px solid var(--primary);
    }
  }
}
</style>
