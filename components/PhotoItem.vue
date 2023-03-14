<template>
  <article>
    <img :src="src" loading="lazy" />
    <img
      src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVR42mNkYAAAAAYAAjCB0C8AAAAASUVORK5CYII="
    />
    <h5 class="title">
      La Fayette : un très gros test pour savoir si trois petits points
    </h5>
  </article>
</template>

<script setup lang="ts">
const props = defineProps({
  src: {
    type: String,
    default: "@/assets/gallery/IMG_20210614_161845.jpg",
  },
});
</script>

<style lang="scss" scoped>
article {
  position: relative;
  top: 0;
  left: 0;
  max-width: 100%;
  max-height: 100%;
  background-color: $secondary;
  overflow: hidden;

  img:nth-child(1) {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  img:nth-child(2) {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    object-fit: fill;
  }

  .title {
    $pa: 0.5rem;
    position: absolute;
    top: 100%;
    padding: $pa;
    width: calc(100% - 2 * $pa);
    color: white;
    font-size: 0.8rem;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    text-shadow: 1px 1px 0 $secondary, -1px -1px 0 $secondary,
      1px -1px 0 $secondary, -1px 1px 0 $secondary;
  }

  &:hover {
    $dimXY: calc(100% + 1rem);
    z-index: 1;
    cursor: pointer;
    top: -0.5rem;
    left: -0.5rem;
    width: $dimXY;
    height: $dimXY;
    max-width: $dimXY;
    max-height: $dimXY;
    box-shadow: 0 0 2rem 0 $primary;
    transition: all 0.3s ease-out;

    .title {
      transition: all 0.3s ease-out;
      transform: translateY(-100%);
    }
  }
}
</style>
