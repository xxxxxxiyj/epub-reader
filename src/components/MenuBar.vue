<template>
  <div>
    <transition name="slide-up">
      <div class="menu-wrap" v-show="showMenu">
        <div class="icon-menu icon"></div>
        <div class="icon-progress icon"></div>
        <div class="icon-brightness icon"></div>
        <div class="icon-font icon"></div>
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
  }
}
</script>
<style lang='scss' scoped>
@import '../assets/styles/global';
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
    &.slide-up-enter,
    &.slide-up-leave-to {
      transform: translate3d(0, 100%, 0);
    }
    &.slide-up-enter-to
    &.slide-up-leave {
      transform: translate3d(0, 0, 0);
    }
    &.slide-up-enter-active,
    &.slide-up-leave-active {
      transition: all .3s linear;
    }
  }
</style>
