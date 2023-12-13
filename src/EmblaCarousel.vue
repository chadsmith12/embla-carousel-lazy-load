<template>
  <div class="embla" ref="emblaNode">
    <div class="embla__container">
      <LazyImage v-for="(image, key) in images" :key="key" :source="image" />
    </div>

    <button @click="slidesInView">Slides in View</button>
  </div>
</template>

<script lang="ts" setup>
import emblaCarouselVue from 'embla-carousel-vue'
import { watchEffect } from 'vue';
import LazyImage from './LazyImage.vue'

defineProps<{
  images: string[]
}>()


const [emblaNode, emblaApi] = emblaCarouselVue()

watchEffect(() => {
  if (!emblaApi.value) {
    return
  }
  console.log(emblaApi.value.slideNodes())
})

function slidesInView() {
  console.log(emblaApi.value?.slidesInView())
}

</script>

<style scoped>
.embla {
  overflow: hidden;
}

.embla__container {
  display: flex;
}

.embla__slide {
  flex: 0 0 100%;
  min-width: 0;
}
</style>
