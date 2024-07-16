# Example

将你自己的组件或内容放入 `Mirror` 组件中即可！  
然后你就看到镜面倒影了！

# How to use

```html
<template>
  <Mirror
    :gradient="gradient"
    :gradientPoint="gradientPoint"
    :blue="blur"
    :opacity="opacity"
    :gap="gap"
  >
    <div class="dv">你自己的组件或内容</div>
  </Mirror>
</template>

<script>
  import Mirror from "edge-mirror/src/Mirror.vue";
  export default {
    components: {
      Mirror,
    },
    data: {
      gradient: false, // 是否开启镜面倒影渐变
      gradientPoint: 0.5, // 镜面倒影渐变点
      blur: 0, // 镜面倒影模糊度，单位px
      opacity: 0.5, // 镜面倒影透明度
      gap: 5, // 镜面倒影与组件之间的距离，单位px
    },
  };
</script>

<style>
  .dv {
    width: 400px;
    height: 400px;
    background-color: goldenrod;
  }
</style>
```
