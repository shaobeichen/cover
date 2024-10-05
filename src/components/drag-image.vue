<script setup>
import { useDraggable } from '@vueuse/core'
import { onMounted, ref } from 'vue'

const props = defineProps({
  text: {
    type: String,
    default: '文字Text'
  },
  initxy: {
    type: Object,
    default: () => ({ x: 0, y: 0 })
  }
})

const el = ref(null)
let parentElement = ref(null)

onMounted(() => {
  parentElement.value = el.value.parentElement
})

const { y } = useDraggable(el, {
  stopPropagation: true,
  initialValue: props.initxy,
  containerElement: parentElement
})
</script>

<template>
  <div
    ref="el"
    style="position: absolute; font-size: 100px; left: 50%; user-select: none"
    :style="{ transform: `translate3d(-50%, ${y}px, 0)` }"
    contenteditable
    v-html="text"
  ></div>
</template>
