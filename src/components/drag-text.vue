<script setup>
import { useDraggable } from '@vueuse/core'
import { ref } from 'vue'

const props = defineProps({
  box: {
    type: Object,
    default: null
  },
  text: {
    type: String,
    default: '文字Text'
  }
})

const el = ref(null)

const { style } = useDraggable(el, {
  stopPropagation: true,
  initialValue: { x: 0, y: 0 },
  containerElement: props.box
})
</script>

<template>
  <div ref="el" :style="style" style="position: fixed; user-select: none" v-html="text"></div>
</template>
