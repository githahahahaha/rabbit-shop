/*
 * @Author: jiea
 * @Date: 2022-05-22 18:31:36
 * @LastEditors: jiea
 * @LastEditTime: 2022-05-22 18:31:36
 * @Description: desc
 */
/*
* @Description: 商品详情
* @path: src/views/goods/components
* @Autor:Huhuuuu
* @LastEditors: Huhuuuu
* Date: 2022-04-24 20:21
* Update: 2022-04-24 20:21
* IDE:WebStorm
*/

<template>
  <div class="goods-detail">
    <!-- 属性 -->
    <ul class="attrs">
      <li v-for="item in goods.details.properties" :key="item.value">
        <span class="dt">{{item.name}}</span>
        <span class="dd">{{item.value}}</span>
      </li>
    </ul>
    <!-- 图片 -->
    <img v-for="item in goods.details.pictures" :key="item" :src="item" alt="">
  </div>
</template>

<script setup>
import { inject } from 'vue'
const goods = inject('goods')

</script>

<style lang="less" scoped>
.goods-detail {
  padding: 40px;
  .attrs {
    display: flex;
    flex-wrap: wrap;
    margin-bottom: 30px;
    li {
      display: flex;
      margin-bottom: 10px;
      width: 50%;
      .dt {
        width: 100px;
        color: #999;
      }
      .dd {
        flex: 1;
        color: #666;
      }
    }
  }
  > img {
    width: 100%;
  }
}
</style>
