<template>
  <time class="time">{{formatDate(date)}}</time>
</template>

<script>
  export default {
    props: {
      date: {
        type: String,
        required: true
      }
    },
    methods: {
      formatDate(date) {
        const options = { year: 'numeric', month: 'long', day: 'numeric' }
        return new Date(date).toLocaleDateString('es', options)
      }
    }
  }
</script>

<style lang="scss">
.time {
  display: block;
  font-size: 1.3rem;
  font-style: italic;
}
</style>