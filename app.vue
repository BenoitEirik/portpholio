<template>
  <div class="appWrapper">
    <Header />
    <NuxtPage class="pageWrapper" />
    <Footer @height="(height) => (footerHeight = height)" />
  </div>
</template>

<script setup lang="ts">
const footerHeight = ref<string>("100vh");
</script>

<style lang="scss">
.appWrapper {
  position: relative;
  z-index: 0;

  .pageWrapper {
    min-height: calc(100vh - v-bind(footerHeight));
    background-color: $primary;
    box-shadow: 0 0 5rem 1rem $primary;
  }
}
</style>
