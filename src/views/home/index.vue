/*
 * @Author: jiea
 * @Date: 2022-05-03 08:32:30
 * @LastEditors: jiea
 * @LastEditTime: 2022-05-11 18:35:48
 * @Description: 首页
 */
<template>
  <div class="xtx-home-page">
    <!-- 首页入口 -->
    <div class="container">
    <div class="home-entry">
        <!-- 左侧分类 -->
        <HomeCategory />
        <!-- 轮播图 -->
        <HomeBanner/>
        <!-- 新鲜好物 -->
        <HomeNew/>
        <!-- 人气推荐 -->
        <HomeHot/>
        <!-- 热门品牌 -->
        <HomeBrand/>
        <!-- 商品区块 -->
        <HomeProduct/>
        <!-- 最新专题 -->
        <HomeSpecial/>
    </div>
  </div>
  </div>
</template>
<script setup>
import HomeCategory from './components/home-categroy.vue'
import HomeBanner from './components/home-banner.vue'
import HomeNew from './components/home-new.vue'
import HomeHot from './components/home-hot.vue'
import HomeBrand from './components/home-brand.vue'
import HomeProduct from './components/home-product.vue'
import HomeSpecial from './components/home-special.vue'

</script>
<style lang="less" scoped></style>
