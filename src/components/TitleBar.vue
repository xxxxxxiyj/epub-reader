<template>
  <div>
    <transition name="slide-down">
      <div class="header-wrap" v-show="showTitle">
        <div class="left">
          <div class="icon-back icon"></div>
        </div>
        <div class="right">
          <div class="icon-person2 icon"></div>
          <div class="icon-more icon"></div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    showTitle: {
      type: Boolean,
      default: false
    }
  }
}
</script>
<style lang='scss' scoped>
@import '../assets/styles/global';
.header-wrap {
    position: fixed;
    top: 0;
    left: 0;
    display: flex;
    @include center;
    width: 100%;
    height: pxTorem(48);
    background: #fff;
    box-shadow: 0 pxTorem(5) pxTorem(5) rgba(0, 0, 0, .15);
    z-index: 6;
    .left {
      flex: 0 0 pxTorem(60);
      margin-left: pxTorem(18);
      .icon-back {
        font-weight: 600;
      }
    }
    .right {
      display: flex;
      justify-content: flex-end;
      flex: 1;
      margin-right: pxTorem(18);
      .icon-more {
        margin-left: pxTorem(12);
      }
    }
    &.slide-down-enter,
    &.slide-down-leave-to {
      transform: translate3d(0, -100%, 0);
    }
    &.slide-down-enter-to,
    &.slide-down-leave {
      transform: translate3d(0, 0, 0);
    }
    &.slide-down-enter-active,
    &.slide-down-leave-active {
      transition: all .3s linear;
    }
  }
</style>
