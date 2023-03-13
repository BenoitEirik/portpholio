<template>
  <footer v-bind:style="{ height: wrapperHeight }">
    <div ref="wrapperRef" id="wrapper">
      <h4 class="signature">Olaf-Marie Sergent</h4>
      <p class="profession">Photographe amateur</p>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { useResizeObserver } from "@vueuse/core";

const wrapperRef = ref(null);
const wrapperHeight = ref("0px");

const emit = defineEmits(["height"]);

useResizeObserver(wrapperRef, () => {
  if (wrapperRef.value !== null) {
    const height = `${(wrapperRef.value as Element).clientHeight}px`;
    emit("height", height);
    wrapperHeight.value = height;
  }
});
</script>

<style lang="scss" scoped>
footer {
  background-color: transparent;
  color: white;
  pointer-events: none;

  #wrapper {
    z-index: -1;
    padding: 2rem 1rem;
    position: fixed;
    inset: auto 0 0 0;
    background-color: $secondary;
    pointer-events: auto;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    background-image: url("@/assets/images/footer/background.svg");
    background-position: bottom;
    background-repeat: no-repeat;
    background-size: 100% auto;
    min-height: $sm;

    .signature {
      font-size: 2rem;
      text-align: center;
    }

    .profession {
      text-align: center;
    }
  }
}
</style>
