/*
 * @Author: jiea
 * @Date: 2022-05-22 18:38:13
 * @LastEditors: jiea
 * @LastEditTime: 2022-05-22 18:38:13
 * @Description: desc
 */
<template>
    <div class="xtx-infinite-loading" ref="container">
        <div class="loading" v-if="loading">
            <span class="img"></span>
            <span class="text">正在加载...</span>
        </div>
        <div class="none" v-if="finished">
            <span class="img"></span>
            <span class="text">亲，没有更多了</span>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
const props = defineProps({
  loading: {
    type: Boolean,
    default: false
  },
  finished: {
    type: Boolean,
    default: false
  }
})
const emit = defineEmits(['infinite'])
const container = ref(null)
useIntersectionObserver(
  container,
  ([{ isIntersecting }], dom) => {
    if (isIntersecting) {
      if (!props.loading && !props.finished) {
        emit('infinite')
      }
    }
  },
  {
    threshold: 0
  }
)
</script>

<style scoped lang='less'>
.xtx-infinite-loading {
    .loading {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 200px;
        .img {
            width: 50px;
            height: 50px;
            background: url(../../assets/images/load.gif) no-repeat center /
                contain;
        }
        .text {
            color: #999;
            font-size: 16px;
        }
    }
    .none {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 200px;
        .img {
            width: 200px;
            height: 134px;
            background: url(../../assets/images/none.png) no-repeat center /
                contain;
        }
        .text {
            color: #999;
            font-size: 16px;
        }
    }
}
</style>
