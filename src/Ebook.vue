<template>
  <div class="ebook">
    <div class="reader-wrap">
      <div id="reader"></div>
      <div class="mask">
        <div class="left" @click="prevPage"></div>
        <div class="center"></div>
        <div class="right" @click="nextPage"></div>
      </div>
    </div>
  </div>
</template>

<script>
import ePub from 'epubjs'
const DOWNLOAD_URL = '/static/pinang.epub'
export default {
  name: 'Ebook',
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
      if(this.rendition) {
        this.rendition.prev()
      }
    },
    nextPage () {
      if(this.rendition) {
        this.rendition.next()
      }
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
}
</style>
