<script setup lang="ts">
interface ButtonGradientProps {
  type?: "normal" | "gradient" | "gradientText";
  rounded?: boolean;
  disable?: boolean;
}

const props = withDefaults(defineProps<ButtonGradientProps>(), {
  disable: false,
  type: "normal",
});
// 圆角
const roundedClass = props.rounded ? " v-rounded" : "";
// 禁用
const disableClass = props.disable ? " v-disable" : "";
// 渐变
const gradientClass =
  props.type === "gradient" && !props.disable ? " v-gradient" : "";
// 文字渐变
const gradientTextClass =
  props.type === "gradientText" && !props.disable ? " v-gradient-text" : "";
</script>

<template>
  <div
    :class="
      'v-button' +
      roundedClass +
      disableClass +
      gradientClass +
      gradientTextClass
    "
  >
    <span class="v-button-span">
      <slot></slot>
    </span>
  </div>
</template>

<style scoped lang="scss">
.v-button {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  width: 120px;
  height: 40px;
  border: 1.5px solid #939393;
  box-sizing: border-box;
  cursor: pointer;
  border-radius: 6px;
  .v-button-span {
    padding: 0 16px;
    font-size: 16px;
    font-style: normal;
    font-weight: 500;
    color: #262626;
  }
  &.v-rounded {
    border-radius: 100px;
  }
  &.v-disable {
    color: #939393;
  }
  &.v-gradient {
    border-color: transparent;
    background-image: linear-gradient(#fff, #fff),
      linear-gradient(to right, #621407, #cc2a0e, #621407);
    background-origin: border-box;
    background-clip: content-box, border-box;
  }
  &.v-gradient-text {
    background: linear-gradient(to right, #981f0b, #cc2a0e, #981f0b);
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
  }
}
.v-button + .v-button {
  margin-left: 16px;
}
</style>
