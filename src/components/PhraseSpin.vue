<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue'

// 定義可用的動畫類型
type AnimationType =
  | 'bounce'
  | 'flash'
  | 'pulse'
  | 'rubberBand'
  | 'shakeX'
  | 'shakeY'
  | 'headShake'
  | 'swing'
  | 'tada'
  | 'wobble'
  | 'jello'
  | 'heartBeat'
  | 'backInDown'
  | 'backInLeft'
  | 'bounceIn'
  | 'bounceInDown'
  | 'bounceInLeft'
  | 'fadeIn'
  | 'fadeInDown'
  | 'fadeInDownBig'
  | 'fadeInLeft'
  | 'fadeInLeftBig'
  | 'fadeInRight'
  | 'fadeInUp'
  | 'fadeInTopLeft'
  | 'fadeInTopRight'
  | 'fadeInBottomLeft'
  | 'fadeInBottomRight'
  | 'flip'
  | 'flipInX'
  | 'flipInY'
  | 'lightSpeedInRight'
  | 'lightSpeedInLeft'
  | 'rotateInDownLeft'
  | 'rotateInDownRight'
  | 'jackInTheBox'
  | 'zoomIn'
  | 'zoomInDown'
  | 'zoomInLeft'
  | 'zoomInRight'
  | 'slideInDown'
  | 'slideInLeft'
  | 'slideInRight'
  | 'slideInUp'

// 定義組件的 Props
interface Props {
  phrases: string[]
  animation: AnimationType
  speed: number
  complete: () => void
}

// 設置 Props 默認值
const props = withDefaults(defineProps<Props>(), {
  animation: 'bounceIn',
  speed: 2000,
  complete: () => { }
})

const currentPhrase = ref<string>('')
let index: number = 0
let intervalId: ReturnType<typeof setInterval> | null = null

// 動畫函數
const animate = (): void => {
  if (props.phrases.length === 0) {
    console.warn('No phrases available to display.')
    return
  }
  currentPhrase.value = props.phrases[index]
  index = (index + 1) % props.phrases.length
  props.complete() // 呼叫 complete 回調函數
}

// 組件掛載時設置動畫和定時器
onMounted((): void => {
  if (props.speed <= 0) {
    console.warn('Invalid speed. It must be a positive number.')
    return
  }
  animate()
  intervalId = setInterval(animate, props.speed)
})

// 組件卸載時清除定時器
onBeforeUnmount((): void => {
  if (intervalId !== null) clearInterval(intervalId)
})
</script>

<template>
  <span :key="index" :class="['animate__animated', `animate__${props.animation}`]" aria-live="polite">
    {{ currentPhrase }}
  </span>
</template>

<style scoped>
.animate__animated {
  display: inline-block
}
</style>