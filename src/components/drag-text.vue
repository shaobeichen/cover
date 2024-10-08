<script setup>
const props = defineProps({
  text: {
    type: String,
    default: '文字Text'
  }
})
</script>

<template>
  <div
    ref="el"
    style="position: absolute; user-select: none; white-space: nowrap"
    contenteditable
    v-html="text"
  ></div>
</template>
