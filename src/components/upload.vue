<template>
  <input type="file" ref="file" @change="uploadBackground" />
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['change'])

const file = ref()
const background = ref('')

const blobToDataURL = (blob, cb) => {
  const reader = new FileReader()
  reader.onload = function (evt) {
    const base64 = evt.target.result
    cb(base64)
  }
  reader.readAsDataURL(blob)
}
const uploadBackground = () => {
  let img = file.value.files[0]
  if (img) {
    blobToDataURL(img, (base64Url) => {
      background.value = base64Url
      emit('change', base64Url)
    })
  }
}
</script>
