/*
 * @Author: jiea
 * @Date: 2022-05-22 18:30:19
 * @LastEditors: jiea
 * @LastEditTime: 2022-05-22 18:30:42
 * @Description: desc
 */
<template>
  <p class="g-name">{{goods.name}}</p>
  <p class="g-desc">{{goods.desc}}</p>
  <p class="g-price">
    <span>{{goods.price}}</span>
    <span>{{goods.oldOrice|| Number(goods.price)+20 }}</span>
  </p>
  <div class="g-service">
    <dl>
      <dt>促销</dt>
      <dd>12月好物放送，App领券购买直降120元</dd>
    </dl>
    <dl>
      <dt>配送</dt>
      <dd>
        至
        <XtxCity @change="changeCity" :fullLocation="fullLocation" />
      </dd>
    </dl>
    <dl>
      <dt>服务</dt>
      <dd>
        <span>无忧退货</span>
        <span>快速退款</span>
        <span>免费包邮</span>
        <a href="javascript:;">了解详情</a>
      </dd>
    </dl>
  </div>
</template>
<script setup>
import { ref } from 'vue'
const props = defineProps({
  goods: {
    type: Object,
    default: () => {}
  }
})
// 默认情况
const provinceCode = ref('610000')
const cityCode = ref('610100')
const countyCode = ref('610112')
const fullLocation = ref('陕西省 西安区 未央区')
// 有默认地址
if (props.goods.userAddresses) {
  const deafultAddr = props.goods.userAddresses.find(addr => addr.isDefault === 1)
  if (deafultAddr) {
    provinceCode.value = deafultAddr.provinceCode
    cityCode.value = deafultAddr.cityCode
    countyCode.value = deafultAddr.countyCode
    fullLocation.value = deafultAddr.fullLocation
  }
}
// 选择城市
const changeCity = (result) => {
  provinceCode.value = result.provinceCode
  cityCode.value = result.cityCode
  countyCode.value = result.countyCode
  fullLocation.value = result.fullLocation
}

</script>

<style lang="less" scoped>
.g-name {
  font-size: 22px;
}
.g-desc {
  color: #999;
  margin-top: 10px;
}
.g-price {
  margin-top: 10px;
  span {
    &::before {
      content: "¥";
      font-size: 14px;
    }
    &:first-child {
      color: @priceColor;
      margin-right: 10px;
      font-size: 22px;
    }
    &:last-child {
      color: #999;
      text-decoration: line-through;
      font-size: 16px;
    }
  }
}
.g-service {
  background: #f5f5f5;
  width: 500px;
  padding: 20px 10px 0 10px;
  margin-top: 10px;
  dl {
    padding-bottom: 20px;
    display: flex;
    align-items: center;
    dt {
      width: 50px;
      color: #999;
    }
    dd {
      color: #666;
      &:last-child {
        span {
          margin-right: 10px;
          &::before {
            content: "•";
            color: @xtxColor;
            margin-right: 2px;
          }
        }
        a {
          color: @xtxColor;
        }
      }
    }
  }
}
</style>
