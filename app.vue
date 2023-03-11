<template>
  <div id="app">
    <Header />

    <div id="pageWrapper">
      <NuxtPage />
    </div>

    <Footer />
  </div>
</template>

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
