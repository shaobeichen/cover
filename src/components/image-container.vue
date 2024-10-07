<template>
  <div style="position: relative; width: 960px; height: 540px; box-shadow: 0 0 1px black">
    <drag-text
      :text="emoji"
      :initxy="{ y: textEmojiY }"
      :style="{ fontSize: `${fontSize + 70}px` }"
    />
    <drag-text
      :text="text1"
      :initxy="{ y: text1Y }"
      :style="{ color: color1, fontSize: `${fontSize}px` }"
    />
    <drag-text
      :text="text2"
      :initxy="{ y: text2Y }"
      :style="{ color: color2, fontSize: `${fontSize}px` }"
    />
    <drag-text
      :text="text3"
      :initxy="{ y: text3Y }"
      :style="{ color: color3, fontSize: `${fontSize}px` }"
    />
    <drag-image
      :src="icon"
      :initxy="{ y: textEmojiY }"
      style="width: 200px; height: 200px; object-fit: cover"
    />
    <img :src="background" style="width: 100%; height: 100%; object-fit: cover" />
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'
import backgroundImage from '@/assets/images/background.jpg'

const props = defineProps({
  colors: {
    type: Array,
    default: () => ['#fff', '#f9a929', '#f55456']
  },
  initxyList: {
    type: Array,
    default: () => [7, 164, 262, 357]
  },
  fontSize: {
    type: Number,
    default: 100
  },
  background: {
    type: String,
    default: ''
  },
  icon: {
    type: String,
    default: ''
  }
})

const emoji = ref('😭')
const text1 = ref('文字一')
const text2 = ref('文字二')
const text3 = ref('文字三')
const color1 = computed(() => props.colors[0])
const color2 = computed(() => props.colors[1])
const color3 = computed(() => props.colors[2])

const textEmojiY = computed(() => props.initxyList[0])
const text1Y = computed(() => props.initxyList[1])
const text2Y = computed(() => props.initxyList[2])
const text3Y = computed(() => props.initxyList[3])
const background = computed(() => props.background || backgroundImage)
const icon = computed(() => props.icon)
</script>
