<template>
  <div ref="pageRef" id="page">
    <PhotoBlock
      v-for="photo in photos"
      :src="photo.src"
      :style="photo.width > photo.height ? 'grid-column-end: span 2;' : ''"
    />
  </div>
</template>

<script lang="ts">
import { Photo } from "@/assets/ts/models";
import ExifReader from "exifreader";

const urlStrings = (
  await Promise.all(
    Object.values(
      import.meta.glob("@/assets/images/gallery/*.{png,jpg,jpeg,PNG,JPEG}", {
        eager: true,
        as: "url",
      })
    )
  )
).reduce((acc, val) => acc.concat(val), []) as string[];

export default defineComponent({
  setup() {
    const photos = ref([] as Photo[]);
    const pageRef = ref(null);

    onMounted(async () => {
      if (!process.client) return;
      await Promise.all(
        urlStrings.map(async (url) => {
          const img = new Image();
          img.src = url;
          await new Promise((resolve) => (img.onload = resolve));

          fetch(url)
            .then((response) => response.arrayBuffer())
            .then(async (arrayBuffer) => {
              const tags = await ExifReader.load(arrayBuffer);
              console.log("tags =", tags.DocumentName?.description || "");
            });

          photos.value.push({
            src: img.src,
            width: img.width,
            height: img.height,
            date: "Date de prise inconnu",
          } as Photo);
        })
      ).finally(() => {
        if (pageRef.value !== null) {
          (pageRef.value as Element)?.classList.add("loaded");
        }
      });
    });

    return {
      pageRef,
      photos,
    };
  },
});
</script>

<style lang="scss" scoped>
#page {
  position: relative;
  margin-block: 5rem 1rem;
  margin-inline: 1rem;
  display: grid;
  gap: 0.25rem;
  grid-template-columns: repeat(8, 1fr);
  grid-auto-rows: calc(12.5vw / 3 * 4);
  grid-auto-flow: dense;

  // Before adding loaded class
  top: 10rem;
  opacity: 0;
}
</style>

<style>
.loaded {
  top: 0 !important;
  opacity: 1 !important;
  transition: all 0.6s ease-out;
}
</style>
