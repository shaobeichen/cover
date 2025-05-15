<template>
  <div style="position: relative; width: 960px; height: 540px; box-shadow: 0 0 1px black">
    <drag-text
      v-for="(item, index) in texts"
      :key="index"
      :text="item.text"
      :style="item"
      style="transform: translate3d(-50%, 0, 0)"
    />
    <drag-text
      v-if="emojiSwitch"
      :text="emoji"
      :style="iconStyle"
      style="transform: translate3d(-50%, 0, 0)"
    />
    <drag-image v-else :src="icon" :style="iconStyle" style="transform: translate3d(-50%, 0, 0)" />
    <img :src="background" style="width: 100%; height: 100%; object-fit: cover" />
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  info: {
    type: Object,
    default: () => ({})
  },
  platform: {
    type: String,
    default: 'desktop'
  },
  emoji: {
    type: String,
    default: ''
  },
  emojiSwitch: {
    type: Boolean,
    default: false
  }
})

const background = computed(() => props.info?.background?.[props.platform]?.src)
const icon = computed(() => props.info?.icon?.[props.platform]?.src)
const iconStyle = computed(() => {
  return {
    ...props.info?.icon[props.platform]
  }
})
const texts = computed(() =>
  props.info?.texts.map((item) => {
    return {
      ...item[props.platform]
    }
  })
)
</script>
