<template>
  <div class="popup-container" v-if="!isClosePopup">
    <div class="mask" ref="mask" :style="{opacity: opacity, backgroundColor: color}"></div>
    <div class="content" ref="content">
      <slot>

      </slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VueComponentPopup',
  props: {
    // 弹层底部透明度
    opacity: {
      type: Number,
      default: 0.8
    },
    // 弹窗底部的颜色
    color: {
      type: String,
      default: '#000000'
    },
    // 是否关闭弹窗
    isClose: {
      type: Boolean,
      default: true
    },
    // 是否需要在点击到弹窗内容之外的位置关闭页面
    isCloseWhenClickMask: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      // 是否关闭弹窗，默认等于 isClose
      isClosePopup: this.isClose
    }
  },
  computed: {

  },
  methods: {
    // 当出现弹窗的时候，禁止滚动
    forbidScroll () {
      document.body.addEventListener('touchmove', function (event) {
        event.preventDefault()
      }, false)
      document.body.style.position = 'fixed'
      document.body.height = '100%'
    },
    // 当关闭弹窗的时候，允许滚动
    allowScroll () {
      document.body.removeEventListener('touchmove', function (event) {
        event.preventDefault()
      }, false)
      document.body.style.position = 'initial'
      document.body.height = 'auto'
    },
    // 点击到弹窗内容之外的时候关闭弹窗
    closeWhenClickMask () {
      if (this.isCloseWhenClickMask) {
        this.$refs.mask && this.$refs.mask.addEventListener('click', () => {
          this.closePopup()
        }, false)
      }
    },
    // 关闭弹窗
    closePopup () {
      this.isClosePopup = true
      this.$emit('close')
    }
  },
  watch: {
    // 监听该属性，根据是否开启弹窗，决定是否允许滚动
    isClosePopup: {
      handler: function (val) {
        if (val) {
          this.allowScroll()
        } else {
          this.forbidScroll()
        }
      },
      immediate: true
    },
    // 监听 isClose 的属性变化，更新 isClosePopup
    isClose: {
      handler: function (val) {
        this.isClosePopup = val
        if (val) {
          this.$emit('close')
        }
      },
      immediate: true
    }
  },
  mounted () {
    // 点击弹窗内容之外，关闭弹窗
    this.closeWhenClickMask()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.popup-container {
  width: 100%;
  height: 100%;
  position: fixed;
  left: 0;
  top: 0;
}
.mask {
  width: 100%;
  height: 100%;
}
.content {
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>
