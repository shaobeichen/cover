<script setup>
import { ref } from 'vue'

const props = defineProps({
  text: {
    type: String,
    default: '文字Text'
  },
  initxy: {
    type: Object,
    default: () => ({ x: '-50%', y: 0 })
  }
})

let y = ref(props.initxy?.y)
let x = ref(props.initxy?.x || '-50%')
</script>

<template>
  <div
    ref="el"
    style="position: absolute; left: 50%; user-select: none; white-space: nowrap"
    :style="{ transform: `translate3d(${x}, ${y}px, 0)` }"
    contenteditable
    v-html="text"
  ></div>
</template>
