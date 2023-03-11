<template>
  <div class="appWrapper">
    <Header />
    <NuxtPage class="pageWrapper" />
    <Footer />
  </div>
</template>

<script setup lang="ts">
const footerHeight = ref<string>("100vh");

function setFooterHeight(value: string) {
  footerHeight.value = value;
}

provide("setFooterHeight", setFooterHeight);
</script>

<style lang="scss">
.appWrapper {
  position: relative;
  z-index: 0;

  .pageWrapper {
    min-height: calc(100vh - v-bind(footerHeight));
    background-color: black;
    box-shadow: 0 0 5rem 1rem black;
  }
}
</style>
