<template>
  <div class="ebook">
    <transition name="slide-down">
      <div class="header-wrap" v-show="showMenuAndTitle">
        <div class="left">
          <div class="icon-back icon"></div>
        </div>
        <div class="right">
          <div class="icon-person2 icon"></div>
          <div class="icon-more icon"></div>
        </div>
      </div>
    </transition>
    <div class="reader-wrap">
      <div id="reader"></div>
      <div class="mask">
        <div class="left" @click="prevPage"></div>
        <div class="center" @click="toggleMenu"></div>
        <div class="right" @click="nextPage"></div>
      </div>
    </div>
    <transition name="slide-up">
      <div class="menu-wrap" v-show="showMenuAndTitle">
        <div class="icon-menu icon"></div>
        <div class="icon-progress icon"></div>
        <div class="icon-brightness icon"></div>
        <div class="icon-font icon"></div>
      </div>
    </transition>
  </div>
</template>

<script>
import ePub from 'epubjs'
const DOWNLOAD_URL = '/static/pinang.epub'
export default {
  data () {
    return {
      showMenuAndTitle: false
    }
  },
  methods: {
    // 电子书的解析与渲染
    showEpub () {
      // 生成Book对象
      this.book = ePub(DOWNLOAD_URL)
      console.log(this.book)
      // 通过Book对象生成Rendition对象
      this.rendition = this.book.renderTo('reader', {
        width: window.innerWidth,
        height: window.innerHeight
      })
      // 通过Rendition.display渲染对象
      this.rendition.display()
    },
    prevPage () {
      if (this.rendition) {
        this.rendition.prev()
      }
    },
    nextPage () {
      if (this.rendition) {
        this.rendition.next()
      }
    },
    toggleMenu () {
      this.showMenuAndTitle = !this.showMenuAndTitle
    }
  },
  mounted () {
    this.showEpub()
  }
}
</script>
<style lang='scss' scoped>
@import 'assets/styles/global';
.ebook {
  position: relative;
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
      margin-left: pxTorem(10);
      .icon-back {
        font-weight: 600;
      }
    }
    .right {
      display: flex;
      justify-content: flex-end;
      flex: 1;
      margin-right: pxTorem(10);
      .icon-more {
        margin-left: pxTorem(5);
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
  .reader-wrap {
    .mask {
      position: absolute;
      top: 0;
      left: 0;
      display: flex;
      width: 100%;
      height: 100%;
      z-index: 5;
      .left {
        flex: 0 0 pxTorem(100);
      }
      .center {
        flex: 1;
      }
      .right {
        flex: 0 0 pxTorem(100);
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
}
</style>
