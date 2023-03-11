<template>
  <article>
    <img :src="src" loading="lazy" />
    <div class="title">
      La Fayette : un très gros test pour savoir si trois petits points
    </div>
  </article>
</template>

<script>
export default defineComponent({
  props: {
    src: {
      type: String,
      default: "@/assets/gallery/IMG_20210614_161845.jpg",
    },
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
  background-color: #3c2a21;
  overflow: hidden;

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  div.title {
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
    text-shadow: 1px 1px 0 black, -1px -1px 0 black, 1px -1px 0 black,
      -1px 1px 0 black;
  }

  &:hover {
    z-index: 1;
    cursor: pointer;
    top: -0.5rem;
    left: -0.5rem;
    width: calc(100% + 1rem);
    height: calc(100% + 1rem);
    max-width: calc(100% + 1rem);
    max-height: calc(100% + 1rem);
    box-shadow: 0 0 2rem 0 black;
    transition: all 0.3s ease-out;

    div.title {
      transition: all 0.3s ease-out;
      top: calc(100% - 3.25rem);
    }
  }
}
</style>
