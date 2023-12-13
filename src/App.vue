<script setup lang="ts">
import { ref } from 'vue'
import EmblaCarousel from './EmblaCarousel.vue'
import iamge1 from './assets/test_images/slide-1.jpg'
import iamge2 from './assets/test_images/slide-2.jpg'
import iamge3 from './assets/test_images/slide-3.jpg'
import iamge4 from './assets/test_images/slide-4.jpg'


const images = ref([iamge1, iamge2, iamge3, iamge4])
</script>

<template>
  <main class="sandbox">
    <section class="sandbox__carousel">
      <EmblaCarousel :images="images" />
    </section>
  </main>
</template>

