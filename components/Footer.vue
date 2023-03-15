<template>
  <footer v-bind:style="{ height: wrapperHeight }">
    <div ref="wrapperRef" id="wrapper">
      <img class="avatar" src="@/assets/images/footer/avatar.jpg" />
      <h4 class="signature">Olaf-Marie Sergent</h4>
      <p class="profession">Photographe amateur</p>
      <img class="gif" src="@/assets/images/footer/eagle.gif" width="50px" />
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
    justify-content: flex-start;
    flex-direction: column;
    align-items: center;
    background-image: url("@/assets/images/footer/background.svg");
    background-position: bottom;
    background-repeat: no-repeat;
    background-size: 100% auto;
    min-height: $xs;

    .avatar {
      margin-bottom: 2rem;
      width: 100px;
      height: 100px;
      border: 2px solid white;
      border-radius: 100%;
    }

    .signature {
      font-size: 2rem;
      text-align: center;
    }

    .profession {
      text-align: center;
    }

    .gif {
      position: absolute;
      top: 25%;
      animation-name: flight-bird;
      animation-duration: 8s;
      animation-timing-function: linear;
      animation-iteration-count: infinite;
      -webkit-animation-delay: 3s;
      -moz-animation-delay: 3s;
      -ms-animation-delay: 3s;
      -o-animation-delay: 3s;
      animation-delay: 3s;
    }

    @keyframes flight-bird {
      0% {
        left: 0;
        transform: translateX(-100%);
      }
      100% {
        left: 100%;
      }
    }

    @media (min-width: $xxl) {
      background-size: max($xxl) auto;
    }
  }
}
</style>
