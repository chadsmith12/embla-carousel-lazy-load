<template>
  <div class="embla__slide">
    <div class="embla__lazy-load" :class="hasLoaded ? 'embla__lazy-load--has-loaded' : ''">
      <span v-if="hasLoaded" class="embla__lazy-load__spinner" />
      <div class="embla__slide_number">
        <span> {{ index + 1 }} </span>
      </div>
      <img class="embla__slide__img embla__lazy-load__image" @load="setLoaded" :src="inView ? source : PLACEHOLDER_SRC"
        :data-src="source" />
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue"

const props = defineProps<{
  source: string,
  inView: boolean,
  index: number
}>()

const PLACEHOLDER_SRC = ref(`data:image/gif;base64,R0lGODlhAQABAAD/ACwAAAAAAQABAAACADs%3D`)
const hasLoaded = ref(false)

// this is called when the image is loaded.
// inView will be true from the parent component when it has finally come into view. From there load it
function setLoaded() {
  if (props.inView) {
    hasLoaded.value = true
  }
}

</script>
