<template>
  <div>
    <el-form ref="form" label-width="100px">
      <el-form-item label="签名颜色">
        <el-select v-model="fontSelect">
          <el-option
            v-for="(item, i) in fontList"
            :key="i"
            :value="item.value"
            :label="item.label"
          ></el-option>
        </el-select>
      </el-form-item>
    </el-form>

    <drag-text />

    <input type="file" ref="file" @change="uploadBackground" />

    <div ref="imageWrapper" :style="{ fontFamily: fontSelect }">
      <div contenteditable v-html="text1"></div>
      <div contenteditable v-html="text2"></div>
      <div contenteditable v-html="text3"></div>
      <div contenteditable v-html="emoji"></div>
      <img :src="background" />
    </div>
    <el-button type="primary" @click="toImage">生成图片</el-button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import html2canvas from 'html2canvas'

const text1 = ref('文字一')
const text2 = ref('文字二')
const text3 = ref('文字三')
const emoji = ref('😭')
const dataURL = ref('')
const imageWrapper = ref()
const file = ref()
const background = ref('')
const fontList = ref([
  {
    label: '荆南波波黑',
    value: 'jing-nan-bo-bo-hei'
  },
  {
    label: '联盟起艺卢帅正锐黑体',
    value: 'lian-meng-qi-yi'
  },
  {
    label: '思源真黑-Bold',
    value: 'si-yuan-zhen-hei-Bold'
  },
  {
    label: '托加里特体-Bold-2',
    value: 'tuo-jia-li-Bold-2'
  },
  {
    label: '小米MiSans-Bold',
    value: 'mi-sans-Bold'
  }
])
const fontSelect = ref(fontList.value[0])

const toImage = () => {
  html2canvas(imageWrapper, {
    backgroundColor: null,
    useCORS: true, // 【重要】开启跨域配置
    allowTaint: true, //允许跨域图片
    taintTest: false //是否在渲染前测试图片
  }).then((canvas) => {
    dataURL.value = canvas.toDataURL('image/png')
  })
}
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
      file.value = ''
    })
  }
}
</script>
