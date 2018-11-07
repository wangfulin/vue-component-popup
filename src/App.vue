<template>
  <div id="app">
    <VueComponentPopup :isClose="isClosePopup" :isCloseWhenClickMask="false" @close="close">
      <div class="popup-content">
        弹窗内容
        <span class="close-btn" ref="close-btn" @click="closePopup">关闭{{isClosePopup}}</span>
      </div>
    </VueComponentPopup>
  </div>
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

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.popup-content {
  width: 200px;
  height: 100px;
  font-size: 32px;
  background-color: red;
}
</style>
