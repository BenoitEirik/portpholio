<template>
  <header>
    <div class="shadow-gradient" />
    <h3>Portphoto</h3>
  </header>
</template>

<style lang="scss" scoped>
header {
  z-index: 10;
  position: fixed;
  inset: 0 0 auto 0;
  padding: 1rem;
  color: white;
  font-size: 1rem;
  font-family: "BiteChocolate";

  .shadow-gradient {
    z-index: -1;
    position: absolute;
    inset: 0 0 auto 0;
    width: 100%;
    height: 0;
    background-color: aqua;
    box-shadow: 0 0 4rem 2rem $primary;
  }
}
</style>
