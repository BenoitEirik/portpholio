<template>
  <footer v-bind:style="{ height: getWrapperHeight }">
    <div ref="wrapperRef" id="wrapper">
      <p class="signature">Olaf-Marie Sergent</p>
      <p class="profession">Photgraphe amateur</p>
    </div>
  </footer>
</template>

<script lang="ts">
export default defineComponent({
  setup() {
    const wrapperRef = ref(null);
    const getWrapperHeight = computed(() => {
      if (wrapperRef.value !== null) {
        const value = (wrapperRef.value as Element).clientHeight + "px";
        const setFooterHeight = inject("setFooterHeight") as Function;
        setFooterHeight(value);
        return value;
      } else {
        return "100px";
      }
    });

    return {
      wrapperRef,
      getWrapperHeight,
    };
  },
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
    background-color: #3c2a21;
    pointer-events: auto;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;

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
