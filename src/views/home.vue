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
      <el-form-item label="">
        <el-button type="primary" @click="toImage">生成图片</el-button>
      </el-form-item>
    </el-form>
  </div>

  <div style="display: flex; width: fit-content; margin: 0 auto">
    <image-container
      id="imageWrapper"
      :info="styleList"
      platform="desktop"
      style="width: 960px; height: 540px"
    />

    <image-container
      id="imageWrapper2"
      :info="styleList"
      platform="mobile"
      style="width: 456px; height: 608px"
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import html2canvas from 'html2canvas'
import backgroundImage from '@/assets/images/background.jpg'
import iconImage from '@/assets/images/icon.png'

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

const background = ref('')
const icon = ref('')

const styleList = computed(() => ({
  background: {
    desktop: {
      src: background.value || backgroundImage
    },
    mobile: {
      src: background.value || backgroundImage
    }
  },
  icon: {
    desktop: {
      src: icon.value || iconImage,
      left: '25%',
      top: '12%',
      width: '230px',
      height: '230px'
    },
    mobile: {
      src: icon.value || iconImage,
      left: '50%',
      top: '12%',
      width: '230px',
      height: '230px'
    }
  },
  texts: [
    {
      desktop: {
        text: '程序员的',
        left: '50%',
        top: '16%',
        fontSize: '140px',
        fontFamily: fontSelect.value,
        fontStyle: 'italic',
        '--color1': '#ff973c',
        backgroundImage: `linear-gradient(35deg, #ffffff, #ffffff, var(--color1), var(--color1), var(--color1))`,
        '-webkit-text-fill-color': 'transparent',
        '-webkit-background-clip': 'text',
        textAlign: 'right',
        width: '70%',
        zIndex: 1,
        letterSpacing: '-6px',
        paddingRight: '20px',
        boxSizing: 'content-box'
      },
      mobile: {
        text: '程序员的',
        left: '48%',
        top: '36%',
        fontSize: '110px',
        fontFamily: fontSelect.value,
        fontStyle: 'italic',
        '--color1': '#ff973c',
        backgroundImage: `linear-gradient(35deg, #ffffff, #ffffff, var(--color1), var(--color1), var(--color1))`,
        '-webkit-text-fill-color': 'transparent',
        '-webkit-background-clip': 'text',
        textAlign: 'center',
        width: '100%',
        zIndex: 1,
        letterSpacing: '-6px',
        paddingRight: '0',
        boxSizing: 'content-box'
      }
    },
    {
      desktop: {
        text: '学英语神器',
        left: '50%',
        top: '43%',
        fontSize: '130px',
        fontFamily: fontSelect.value,
        fontStyle: 'italic',
        '--color1': 'rgb(255 106 161)',
        backgroundImage: `linear-gradient(35deg, #ffffff, #ffffff, var(--color1), var(--color1), var(--color1))`,
        '-webkit-text-fill-color': 'transparent',
        '-webkit-background-clip': 'text',
        textAlign: 'right',
        width: '70%',
        zIndex: 1,
        letterSpacing: '-6px',
        paddingRight: '20px',
        boxSizing: 'content-box'
      },
      mobile: {
        text: '学英语神',
        left: '48%',
        top: '54%',
        fontSize: '100px',
        fontFamily: fontSelect.value,
        fontStyle: 'italic',
        '--color1': 'rgb(255 106 161)',
        backgroundImage: `linear-gradient(35deg, #ffffff, #ffffff, var(--color1), var(--color1), var(--color1))`,
        '-webkit-text-fill-color': 'transparent',
        '-webkit-background-clip': 'text',
        textAlign: 'center',
        width: '100%',
        zIndex: 1,
        letterSpacing: '-6px',
        paddingRight: '0',
        boxSizing: 'content-box'
      }
    }
  ]
}))
const updateBackground = (value) => {
  background.value = value
}
const updateIcon = (value) => {
  icon.value = value
}

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
    downloadImage(canvas.toDataURL('image/png'), '16')
  })
  html2canvas(document.querySelector('#imageWrapper2'), {
    backgroundColor: null,
    useCORS: true, // 【重要】开启跨域配置
    allowTaint: true, //允许跨域图片
    taintTest: false //是否在渲染前测试图片
  }).then((canvas) => {
    downloadImage(canvas.toDataURL('image/png'), '9')
  })
}
</script>
