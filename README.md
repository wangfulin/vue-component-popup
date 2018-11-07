# vue-component-popup

> 弹层组件

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

## 功能介绍
该组件主要用户页面的弹窗功能，主要提供的能力有：
1. 包含弹窗底部的半透明阴影，可以自定义颜色和透明度
2. 暴露关闭事件，在关闭的时候用户可以自定义关闭的事件处理
3. 暴露 isClose 的属性，用户可以通过控制传入到这个属性的值来决定是否关闭弹窗
4. 可以通过 isCloseWhenClickMask 来控制是否需要在点击非弹窗内容的部分是否需要关闭弹窗

## 示例
```
<template>
  <VueComponentPopup :isClose="false" :isCloseWhenClickMask="true" @close="close">
    <div class="popup-content">
      弹窗内容
    </div>
  </VueComponentPopup>
</template>

<script>
  import VueComponentPopup from './components/Popup'

  export default {
    name: 'App',
    components: {
      VueComponentPopup
    },
    data: () => {
      return {
        isClosePopup: false
      }
    },
    methods: {
      close () {
        alert('关闭弹窗回调')
      },
      closePopup () {
        this.isClosePopup = true
      }
    }
  }
</script>
```

## 展示
![](https://gw.alipayobjects.com/zos/rmsportal/oVTpKduNuKrsOWJhustA.gif)


For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
