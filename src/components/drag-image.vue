<script setup>
import { ref } from 'vue'

const props = defineProps({
  src: {
    type: String,
    default: ''
  },
  initxy: {
    type: Object,
    default: () => ({ x: 0, y: 0 })
  }
})

let y = ref(props.initxy?.y)
let x = ref(props.initxy?.x || '-50%')
</script>

<template>
  <img
    v-if="src"
    ref="el"
    style="position: absolute; font-size: 100px; left: 50%; user-select: none; user-drag: none"
    :style="{ transform: `translate3d(${x}, ${y}px, 0)` }"
    :src="src"
  />
</template>
