<!--
 * @Author: chenjie
 * @Date: 2022-03-06 21:42:55
 * @LastEditors: jiea
 * @LastEditTime: 2022-05-03 08:32:48
 * @FilePath: \rabbit-shop\src\views\home\components\home-banner.vue
 * @Description:
 *
 * Copyright (c) 2022 by chenjie, All Rights Reserved.
-->
<template>
  <div class="home-banner">
    <XtxCarousel :sliders="sliders.data" auto-play />
  </div>
</template>

<script setup>
import { reactive } from 'vue'
import { findBanner } from '@/api/home'
const sliders = reactive({ data: [] })
// 获取轮播图数据
findBanner().then(data => {
  sliders.data = data.result
})

</script>
<style scoped lang="less">
.home-banner {
  width: 1240px;
  height: 500px;
  position: absolute;
  left: 0;
  top: 0;
  z-index: 98;
}
.xtx-carousel {
  :v-deep(.carousel-btn.prev)  {
    left: 270px;
  }
  :v-deep (.carousel-indicator) {
    padding-left: 250px;
  }
}
</style>
