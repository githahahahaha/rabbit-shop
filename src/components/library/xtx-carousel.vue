/*
 * @Author: jiea
 * @Date: 2022-05-22 18:39:27
 * @LastEditors: jiea
 * @LastEditTime: 2022-05-22 18:39:27
 * @Description: desc
 */
/*
 * @Description: file content
 * @path: src\components\library\xtx-carousel.vue
 * @Autor:jie
 * @LastEditors: jie
 * @Time: 2022-04-23 20:44:38
 */
<template>
  <div class="xtx-carousel" @mouseenter="stop()" @mouseleave="start()">
    <ul class="carousel-body">
      <!-- 图片 -->
      <li
        class="carousel-item "
        v-for="(item, i) in sliders"
        :key="i"
        :class="{ fade: index === i }"
      >
        <RouterLink v-if="item.hrefUrl" :to="item.hrefUrl">
          <img :src="item.imgUrl" alt="" />
        </RouterLink>
        <div v-else class="slider">
          <RouterLink v-for="goods in item" :key="goods.id" :to="`/product/${goods.id}`">
            <img :src="goods.picture" alt="" />
            <p class="name ellipsis">{{goods.name}}</p>
            <p class="price">&yen;{{goods.price}}</p>
          </RouterLink>
        </div>
      </li>
    </ul>
    <!-- 上一张 -->
    <a href="javascript:;" class="carousel-btn prev" @click="toggle(-1)"
      ><i class="iconfont icon-angle-left"></i
    ></a>
    <!-- 下一张 -->
    <a href="javascript:;" class="carousel-btn next" @click="toggle(1)"
      ><i class="iconfont icon-angle-right"></i
    ></a>
    <!-- 激活点 -->
    <div class="carousel-indicator">
      <span
        v-for="(i2, i) in sliders.length"
        :key="i"
        :class="{ active: index === i }"
        @click="index = i"
      ></span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'XtxCarousel'
}
</script>
<script setup>
import { onUnmounted, ref, watch } from 'vue'

const props = defineProps({
  // 轮播图数据
  sliders: {
    type: Array,
    default: () => []
  },
  // 是否自动轮播
  autoPlay: {
    type: Boolean,
    default: () => false
  },
  // 间隔时长
  duration: {
    type: Number,
    default: () => 3000
  }
})

const index = ref(0)
// 自动轮播
let timer = null
const autoPlayFn = () => {
  clearInterval(timer)
  timer = setInterval(() => {
    index.value++
    if (index.value >= props.sliders.length) {
      index.value = 0
    }
  }, props.duration)
}
// 监听 sliders 数据变化  如果有数据 并且 autoPlay 是 true
watch(
  () => props.sliders,
  newVal => {
    if (newVal.length && props.autoPlay) {
      autoPlayFn()
    }
  },
  { immediate: true }
)
// 鼠标进入暂停播放 离开开启自动播放
const stop = () => {
  if (timer) clearInterval(timer)
}

const start = () => {
  if (props.sliders.length && props.autoPlay) {
    autoPlayFn()
  }
}

// 切换上一张下一张
const toggle = step => {
  // 将要改变的索引
  const newIndex = index.value + step
  if (newIndex > props.sliders.length - 1) {
    index.value = 0
    return
  }
  if (newIndex < 0) {
    index.value = props.sliders.length - 1
    return
  }
  // 正常
  index.value = newIndex
}

// 组件卸载 清除定时器
onUnmounted(() => {
  clearInterval(timer)
})
</script>
<style scoped lang="less">
.xtx-carousel {
  width: 100%;
  height: 100%;
  min-width: 300px;
  min-height: 150px;
  position: relative;
  .carousel {
    &-body {
      width: 100%;
      height: 100%;
    }
    &-item {
      width: 100%;
      height: 100%;
      position: absolute;
      left: 0;
      top: 0;
      opacity: 0;
      transition: opacity 0.5s linear;
      &.fade {
        opacity: 1;
        z-index: 1;
      }
      // 轮播商品
      .slider {
        display: flex;
        justify-content: space-around;
        padding: 0 40px;
        > a {
          width: 240px;
          text-align: center;
          img {
            padding: 20px;
            width: 230px!important;
            height: 230px!important;
          }
          .name {
            font-size: 16px;
            color: #666;
            padding: 0 40px;
          }
          .price {
            font-size: 16px;
            color: @priceColor;
            margin-top: 15px;
          }
        }
      }
      img {
        width: 100%;
        height: 100%;
      }
    }
    &-indicator {
      position: absolute;
      left: 0;
      bottom: 20px;
      z-index: 2;
      width: 100%;
      text-align: center;
      span {
        display: inline-block;
        width: 12px;
        height: 12px;
        background: rgba(0, 0, 0, 0.2);
        border-radius: 50%;
        cursor: pointer;
        ~ span {
          margin-left: 12px;
        }
        &.active {
          background: #fff;
        }
      }
    }
    &-btn {
      width: 44px;
      height: 44px;
      background: rgba(0, 0, 0, 0.2);
      color: #fff;
      border-radius: 50%;
      position: absolute;
      top: 228px;
      z-index: 2;
      text-align: center;
      line-height: 44px;
      opacity: 0;
      transition: all 0.5s;
      &.prev {
        left: 20px;
      }
      &.next {
        right: 20px;
      }
    }
  }
  &:hover {
    .carousel-btn {
      opacity: 1;
    }
  }
}
</style>
