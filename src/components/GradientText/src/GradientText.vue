<script lang="ts" setup>
type TextType = 'error' | 'info' | 'warning' | 'success'
type WeightType =
  | 100
  | 200
  | 300
  | 400
  | 500
  | 600
  | 700
  | 800
  | 900
  | 'normal'
  | 'bold'
type RotateType = 'to left' | 'to right' | 'to bottom' | 'to top' | number
interface IGradient {
  rotate: RotateType // 线性渐变方向
  start: string // 开始的色值
  end: string // 结束的色值
}
interface Props {
  type?: TextType
  size?: string
  gradient?: IGradient
  weight?: WeightType
}
const props = defineProps<Props>()
</script>
<template>
  <span
    class="ywz-gradient-text"
    :class="[props.type, props.gradient ? 'custom-gradient' : '']"
    :style="{
      '--size': props.size ?? '16px',
      '--weight': props.weight ?? '400',
      '--rotate':
        typeof props.gradient?.rotate === 'number'
          ? props.gradient?.rotate + 'deg'
          : props.gradient?.rotate,
      '--start': props.gradient?.start,
      '--end': props.gradient?.end,
    }"
  >
    <!-- 默认插槽，也就是文字 -->
    <slot></slot>
  </span>
</template>
<style>
.ywz-gradient-text {
  display: inline-block;
  font-weight: var(--weight);
  background-clip: text;
  font-size: var(--size);
  -webkit-background-clip: text;
  color: transparent;
  white-space: nowrap;
}
.error {
  background-image: linear-gradient(
    252deg,
    rgba(208, 48, 80, 0.6) 0%,
    #d03050 100%
  );
}
.info {
  background-image: linear-gradient(
    252deg,
    rgba(32, 128, 240, 0.6) 0%,
    #2080f0 100%
  );
}
.warning {
  background-image: linear-gradient(
    252deg,
    rgba(240, 160, 32, 0.6) 0%,
    #f0a020 100%
  );
}
.success {
  background-image: linear-gradient(
    252deg,
    rgba(24, 160, 88, 0.6) 0%,
    #18a058 100%
  );
}
.custom-gradient {
  background-image: linear-gradient(
    var(--rotate),
    var(--start) 0%,
    var(--end) 100%
  );
}
</style>
