<template>
  <div id="app">
    <Header />

    <div id="pageWrapper">
      <NuxtPage :footerHeight="footerHeight" />
    </div>

    <Footer />
  </div>
</template>

<script lang="ts">
export default defineComponent({
  setup() {
    const footerHeight = ref<string>("0px");

    const setFooterHeight = (value: string) => {
      footerHeight.value = value;
    };

    provide("setFooterHeight", setFooterHeight);

    return {
      footerHeight,
    };
  },
});
</script>

<style lang="scss">
#app {
  position: relative;
  z-index: 0;

  #pageWrapper {
    background-color: black;
    box-shadow: 0 0 5rem 1rem black;
  }
}
</style>
