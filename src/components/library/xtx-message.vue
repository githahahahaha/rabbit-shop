/*
* @path: src/components/library
* @Autor:jiea
* @LastEditors: jiea
* Date: 2022-05-10 19:38
* @LastEditTime: 2022-05-11 19:04:42
* IDE:WebStorm
* @Description: 小兔仙提示组件
*/
<template>
  <Transition name="down">
    <div class="xtx-message" :style="style[type]" v-show="visible">
      <!-- 上面绑定的是样式 -->
      <!-- 不同提示图标会变 -->
      <i class="iconfont" :class="[style[type].icon]"></i>
      <span class="text">{{ text }}</span>
    </div>
  </Transition>
</template>

<script>
export default {
  name: 'XtxMessage'
}
</script>
<script setup>
import { onMounted, ref } from 'vue'

defineProps({
  // 提示文字
  text: {
    type: String,
    default: ''
  },
  //   warn 警告 error 错误 success 成功
  type: {
    type: String,
    default: 'warn'
  }
})
// 定义一个对象，包含三种情况的样式，对象key就是类型字符串
const style = {
  warn: {
    icon: 'icon-warning',
    color: '#E6A23C',
    backgroundColor: 'rgb(253, 246, 236)',
    borderColor: 'rgb(250, 236, 216)'
  },
  error: {
    icon: 'icon-shanchu',
    color: '#F56C6C',
    backgroundColor: 'rgb(254, 240, 240)',
    borderColor: 'rgb(253, 226, 226)'
  },
  success: {
    icon: 'icon-queren2',
    color: '#67C23A',
    backgroundColor: 'rgb(240, 249, 235)',
    borderColor: 'rgb(225, 243, 216)'
  }
}
// 控制显示隐藏 默认是隐藏 组件挂载完毕显示
const visible = ref(false)
onMounted(() => {
  visible.value = true
})
</script>

<style scoped lang="less">
.down {
    &-enter {
        &-from {
          transform: translate3d(0,-75px,0);
          opacity: 0;
        }
        &-active {
          transition: all 0.5s;
        }
        &-to {
          transform: none;
          opacity: 1;
        }
   }
}
.xtx-message {
  width: 300px;
  height: 50px;
  position: fixed;
  z-index: 9999;
  left: 50%;
  margin-left: -150px;
  top: 25px;
  line-height: 50px;
  padding: 0 25px;
  border: 1px solid #e4e4e4;
  background: #f5f5f5;
  color: #999;
  border-radius: 4px;

  i {
    margin-right: 4px;
    vertical-align: middle;
  }

  .text {
    vertical-align: middle;
  }
}
</style>
