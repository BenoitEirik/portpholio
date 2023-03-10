<template>
  <article :style="`background-image: url(${src});`">
    <div class="title">Épi de blé</div>
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
  background-position: center;
  background-size: cover;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: stretch;

  div.title {
    position: relative;
    top: 3rem;
    margin: 0.5rem;
    color: white;
    font-size: 1.5rem;
    font-weight: 100;
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
    border-radius: 4px;
    transition: all 0.3s ease-out;

    div.title {
      transition: all 0.3s ease-out;
      top: 0;
    }
  }
}
</style>
