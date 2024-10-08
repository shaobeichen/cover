<template>
  <div style="position: relative; width: 960px; height: 540px; box-shadow: 0 0 1px black">
    <drag-text
      v-for="(item, index) in texts"
      :key="index"
      :text="item.text"
      :style="item"
      style="transform: translate3d(-50%, 0, 0)"
    />
    <drag-image :src="icon" :style="iconStyle" style="transform: translate3d(-50%, 0, 0)" />
    <img :src="background" style="width: 100%; height: 100%; object-fit: cover" />
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  info: {
    type: Object,
    default: () => ({})
  },
  platform: {
    type: String,
    default: 'desktop'
  }
})

const background = computed(() => props.info?.background)
const icon = computed(() => props.info?.icon?.src)
const iconStyle = computed(() => {
  return {
    width: props.info?.icon?.width,
    height: props.info?.icon?.height,
    left: props.info?.icon?.left?.[props.platform],
    top: props.info?.icon?.top?.[props.platform]
  }
})
const texts = computed(() =>
  props.info?.texts.map((item) => {
    return {
      ...item,
      left: item.left?.[props.platform],
      top: item.top?.[props.platform]
    }
  })
)
</script>
