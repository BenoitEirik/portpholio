<template>
  <div ref="pageRef" class="page">
    <div class="presentation">
      <h1>Bienv]enue</h1>
      <p>Voici l'ensemble de mes photos. Bonne visite !</p>
    </div>

    <div v-if="!loading" class="grid">
      <PhotoBlock
        v-for="photo in photos"
        :src="photo.src"
        :style="photo.width > photo.height ? 'grid-column-end: span 2;' : ''"
      />
    </div>
    <div v-else class="loading">
      <Loader />
    </div>
  </div>
</template>

<script setup lang="ts">
import { Photo } from "@/assets/ts/models";
import exifr from "exifr";

const photos = ref([] as Photo[]);
const pageRef = ref(null);
const loading = ref<boolean>(true);

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
  loading.value = false;
});
</script>

<style lang="scss" scoped>
.page {
  padding-bottom: 2rem;

  .presentation {
    position: relative;
    padding-block: 5rem 1rem;
    padding-inline: 1rem;
    text-align: center;
    color: white;
    animation: appear 1s;

    h1:nth-child(1) {
      z-index: 2;
      position: relative;
      font-size: 2rem;
      text-shadow: 2px 2px 0 $primary, -2px -2px 0 $primary, 2px -2px 0 $primary,
        -2px 2px 0 $primary;
      &::before {
        position: absolute;
        z-index: -1;
        content: "Bienv]enue";
        background: linear-gradient(
          180deg,
          rgba(2, 0, 36, 1) 50%,
          rgba(255, 255, 255, 1) 100%
        );
        background-clip: text;
        color: transparent;
        text-shadow: none;
        top: 4px;
      }
    }
    p:nth-child(1) {
      font-size: 1rem;
    }
  }

  .loading {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: flex;
    width: 100%;
    justify-content: center;
  }

  // Mobile-first
  .grid {
    position: relative;
    margin: 1rem;
    display: grid;
    gap: 0.25rem;
    grid-template-columns: repeat(1, 1fr);
    grid-auto-rows: calc(100vw / 3 * 4);
    grid-auto-flow: dense;
    border-radius: 4px;
    overflow: hidden;
    &:hover {
      overflow: visible;
    }
  }

  @media (min-width: 768px) {
    .grid {
      grid-template-columns: repeat(8, 1fr);
      grid-auto-rows: calc(12.5vw / 3 * 4);
      grid-auto-flow: dense;
    }
  }

  @keyframes appear {
    from {
      opacity: 0;
      top: -20px;
    }
    to {
      opacity: 1;
      top: 0px;
    }
  }
}
</style>
