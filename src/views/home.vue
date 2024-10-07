<template>
  <div style="max-width: 500px; margin: 0 auto">
    <el-form ref="form" label-width="100px">
      <el-form-item label="字体">
        <el-select v-model="fontSelect">
          <el-option
            v-for="(item, i) in fontList"
            :key="i"
            :value="item.value"
            :label="item.label"
          ></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="背景">
        <upload @change="updateBackground" />
      </el-form-item>
      <el-form-item label="主icon">
        <upload @change="updateIcon" />
      </el-form-item>
      <el-form-item label="选择风格">
        <el-select v-model="styleSelect">
          <el-option
            v-for="item in styleList"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          />
        </el-select>
      </el-form-item>
      <el-form-item label="文字颜色">
        <el-color-picker v-model="color1" show-alpha />
        <el-color-picker v-model="color2" show-alpha />
        <el-color-picker v-model="color3" show-alpha />
      </el-form-item>
      <el-form-item label="">
        <el-button type="primary" @click="toImage">生成图片</el-button>
      </el-form-item>
    </el-form>
  </div>

  <div style="display: flex; width: fit-content; margin: 0 auto">
    <image-container
      id="imageWrapper"
      :colors="[color1, color2, color3]"
      :initxy-list="currentInitxyList[0]"
      :background="background"
      :icon="icon"
      :style="{ fontFamily: fontSelect }"
      style="width: 960px; height: 540px"
    />
    &
    <image-container
      id="imageWrapper2"
      :colors="[color1, color2, color3]"
      :initxy-list="currentInitxyList[1]"
      :background="background"
      :icon="icon"
      :fontSize="70"
      style="width: 456px; height: 608px"
      :style="{ fontFamily: fontSelect }"
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import html2canvas from 'html2canvas'

const color1 = ref('#fff')
const color2 = ref('#f9a929')
const color3 = ref('#f55456')

const dataURL = ref('')
const dataURL2 = ref('')
const background = ref('')
const icon = ref('')
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
const fontSelect = ref(fontList.value[0].value)
const styleList = ref([
  {
    value: 1,
    label: '上下风格'
  },
  {
    value: 2,
    label: '左右风格'
  }
])
const styleSelect = ref(styleList.value[0].value)
const initxyListMap = {
  1: [
    [-20, 164, 262, 357],
    [60, 220, 297, 374]
  ],
  2: [
    [0, 0, 0, 0],
    [60, 164, 262, 357]
  ]
}
const currentInitxyList = computed(() => initxyListMap[styleSelect.value || 1])

const downloadImage = (value, name) => {
  const link = document.createElement('a')
  link.href = value
  link.download = name + '.png' // 设置下载文件名
  document.body.appendChild(link)
  link.click() // 触发点击事件
  document.body.removeChild(link) // 移除链接
}

const toImage = () => {
  html2canvas(document.querySelector('#imageWrapper'), {
    backgroundColor: null,
    useCORS: true, // 【重要】开启跨域配置
    allowTaint: true, //允许跨域图片
    taintTest: false //是否在渲染前测试图片
  }).then((canvas) => {
    dataURL.value = canvas.toDataURL('image/png')
    downloadImage(dataURL.value, '16')
  })
  html2canvas(document.querySelector('#imageWrapper2'), {
    backgroundColor: null,
    useCORS: true, // 【重要】开启跨域配置
    allowTaint: true, //允许跨域图片
    taintTest: false //是否在渲染前测试图片
  }).then((canvas) => {
    dataURL2.value = canvas.toDataURL('image/png')
    downloadImage(dataURL2.value, '9')
  })
}

const updateBackground = (value) => {
  background.value = value
}
const updateIcon = (value) => {
  icon.value = value
}
</script>
