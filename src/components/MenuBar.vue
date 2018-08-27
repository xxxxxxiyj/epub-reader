<template>
  <div class="container">
    <transition name="slide-up">
      <div class="menu-wrap" :class="{'hide-menu-shadow' : showSetting || !showMenu}" v-show="showMenu">
        <div class="icon-menu icon"></div>
        <div class="icon-progress icon"></div>
        <div class="icon-brightness icon"></div>
        <div class="icon-font icon" @click="showSettingBar"></div>
      </div>
    </transition>
    <transition name="slide-up">
      <div class="setting-wrap" v-show="showSetting">
        <button class="minus-fontsize font-set" @click="minusFontSize">A-</button>
        <button class="add-fontsize font-set" @click="addFontSize">A+</button>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    showMenu: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      showSetting: false
    }
  },
  methods: {
    showSettingBar () {
      this.showSetting = !this.showSetting
    },
    hideSettingBar () {
      this.showSetting = false
    },
    addFontSize () {
      this.$emit('addFont')
    },
    minusFontSize () {
      this.$emit('minusFont')
    }
  }
}
</script>
<style lang='scss' scoped>
@import '../assets/styles/global';
.container {
  .setting-wrap {
    @include center;
    position: fixed;
    bottom: pxTorem(48);
    left: 0;
    width: 100%;
    height: pxTorem(60);
    background-color: #fff;
    box-shadow: 0 pxTorem(-5) pxTorem(5) rgba(0, 0, 0, .15);
    z-index: 6;
    .font-set {
      @include center;
      width: pxTorem(100);
      height: pxTorem(35);
      font-size: pxTorem(16);
      border: 1px solid #999;
      outline: none;
      background-color: #fff;
      box-shadow: 0 pxTorem(3) pxTorem(3) rgba(0, 0, 0, .15);
      &.minus-fontsize {
        border-top-left-radius: pxTorem(15);
        border-bottom-left-radius: pxTorem(15);
      }
      &.add-fontsize {
        border-top-right-radius: pxTorem(15);
        border-bottom-right-radius: pxTorem(15);
      }
    }
  }
  .menu-wrap {
    position: fixed;
    bottom: 0;
    left: 0;
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 100%;
    height: pxTorem(48);
    background: #fff;
    box-shadow: 0 pxTorem(-5) pxTorem(5) rgba(0, 0, 0, .15);
    z-index: 5;
    &.hide-menu-shadow {
      box-shadow: none;
    }
  }
  .slide-up-enter,
  .slide-up-leave-to {
    transform: translate3d(0, pxTorem(108), 0);
  }
  .slide-up-enter-to
  .slide-up-leave {
    transform: translate3d(0, 0, 0);
  }
  .slide-up-enter-active,
  .slide-up-leave-active {
    transition: all .3s linear;
  }
}
</style>
