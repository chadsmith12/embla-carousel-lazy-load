<template>
  <div class="embla">
    <div class="embla__viewport" ref="emblaNode">
      <div class="embla__container">
        <LazyImage v-for="(image, key) in images" :key="key" :source="image" :index="key"
          :in-view="slidesInView.indexOf(key) > -1" />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import emblaCarouselVue, { EmblaCarouselType } from 'embla-carousel-vue'
import { watchEffect, ref } from 'vue';
import LazyImage from './LazyImage.vue'

defineProps<{
  images: string[]
}>()


const [emblaNode, emblaApi] = emblaCarouselVue()
const slidesInView = ref<number[]>([])

// watch for when the mblaApi becomes active for us.
watchEffect(() => {
  if (!emblaApi.value) {
    return
  }

  // we know it's active now, lets listen to some events from the api
  emblaApi.value.on('slidesInView', updateSlidesInView)
  emblaApi.value.on('reInit', updateSlidesInView)
})


function updateSlidesInView(api: EmblaCarouselType) {
  // we we already have all the slides in view, we can just stop listening to this event now.
  if (slidesInView.value.length === api.slideNodes().length) {
    api.off('slidesInView', updateSlidesInView)
  }

  // lets get all the updated slides in view that we don't know of yet.
  // If we find any, add them to our list of slides to show
  const inView = api.slidesInView().filter((index: number) => !slidesInView.value.includes(index));
  if (!inView) {
    return
  }

  // only artificially slowing it down to show it
  if (inView.includes(0)) {
    slidesInView.value.push(...inView)
    return
  }
  setTimeout(() => { slidesInView.value.push(...inView) }, 200)
}

</script>

