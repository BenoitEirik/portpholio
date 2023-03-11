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
import exifr from "exifr";

export default defineComponent({
  setup() {
    const photos = ref([] as Photo[]);
    const pageRef = ref(null);

    onMounted(async () => {
      const imgs = Object.values<Record<string, any>>(
        import.meta.glob("@/assets/images/gallery/*.{png,jpg,jpeg,PNG,JPEG}", {
          eager: true,
          as: "url",
        })
      ).map((r) => r as unknown as string);

      imgs.forEach(async (url) => {
        const img = new Image();
        img.src = url;
        await new Promise((resolve) => (img.onload = resolve));

        exifr
          .parse(url)
          .then((output) => console.log("Camera:", output.Make, output.Model));

        photos.value.push({
          src: img.src,
          width: img.width,
          height: img.height,
          date: "Date de prise inconnu",
        } as Photo);
      });

      if (pageRef.value !== null) {
        (pageRef.value as Element)?.classList.add("loaded");
      }
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
  padding-block: 5rem 2rem;
  padding-inline: 1rem;
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
