
<script >
import { h } from 'vue'
export default {
  name: 'XtxBread',
  /**
   * 用法
   * 1.template 标签去除，单文件组件。
   * 2.返回值就是组件内容。
   * 3.vue2.0 的 h 函数传参进来的，vue3.0 的 h 函数导入进来
   * 4. h 第一个参数：标签名字，第二个参数：标签属性对象。第三个参数：子节点。
   * 需求
   * 1.创建 xtx-bread 父容器。
   * 2.获取默认插槽内容。
   * 3.去除 xtx-bread-item 组件的 i 标签，应该有 render 函数来组织。
   * 4.遍历插槽中的 item，得到一个动态创建的结点，最后一个 item 不加 i 标签。
   * 5.把动态创建的节点渲染在 xtx-bread 标签中。
   */
  render () {
    const items = this.$slots.default()
    const dymanicItems = []
    items.forEach((item, i) => {
      dymanicItems.push(item)
      if (i < items.length - 1) {
        dymanicItems.push(h('i', { class: 'iconfont icon-angle-right' }))
      }
    })
    return h('div', { class: 'xtx-bread' }, dymanicItems)
  }
}
</script>

<style  lang='less'>
// 去除 scoped 属性， 目的让样式作用到 xtx-bread-item 组件
.xtx-bread{
  display: flex;
  padding: 25px 10px;
  &-item {
    span {
      color: #666;
      transition: all .4s;
      &:hover {
        color: @xtxColor;
      }
    }
  }
  i {
    font-size: 12px;
    margin-left: 5px;
    margin-right: 5px;
    line-height: 22px;
  }
}
</style>
