<script setup>
const props = defineProps({
  src: {
    type: String,
    default: ''
  }
})
</script>

<template>
  <img
    v-if="src"
    ref="el"
    style="
      position: absolute;
      user-select: none;
      white-space: nowrap;
      user-drag: none;
      object-fit: cover;
    "
    :src="src"
  />
</template>
