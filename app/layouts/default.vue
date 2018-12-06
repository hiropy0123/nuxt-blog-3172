<template>
  <div class="wrapper">
    <TheHeader />
    <nuxt class="container" />
  </div>
</template>

<script>
import TheHeader from '~/components/TheHeader'

export default {
  components: {
    TheHeader
  }
}
</script>

<style>
.wrapper {
  max-width: 1080px;
  padding: 0 20px;
  margin: auto;
}
</style>