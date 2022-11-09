<template>
  <div class="heading">
    <h1 class="heading__title">{{ title }}</h1>
    <p class="heading__text">{{ text }}</p>
  </div>
</template>

<script>
export default {
  name: "Heading",
  props: ['title', 'text']
}
</script>

<style lang="scss" scoped>
.heading {
  margin-bottom: 2rem;

  &__title {
    margin-bottom: 0.25rem;
  }

  &__text {

  }
}
</style>