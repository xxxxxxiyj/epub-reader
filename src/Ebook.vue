<template>
  <div class="ebook">
    <title-bar :showTitle="showMenuAndTitle"></title-bar>
    <div class="reader-wrap">
      <div id="reader" :style="{fontSize: fontSize + 'px'}"></div>
      <div class="mask">
        <div class="left" @click="prevPage"></div>
        <div class="center" @click="toggleMenu"></div>
        <div class="right" @click="nextPage"></div>
      </div>
    </div>
    <menu-bar :showMenu="showMenuAndTitle" ref="hideSetting" @addFont="addFontSize" @minusFont="minusFontSize"></menu-bar>
  </div>
</template>

<script>
import TitleBar from '@/components/TitleBar'
import MenuBar from '@/components/MenuBar'
import ePub from 'epubjs'
const DOWNLOAD_URL = '/static/pinang.epub'
export default {
  components: {
    TitleBar,
    MenuBar
  },
  data () {
    return {
      maxFontSize: 24,
      minFontSize: 12,
      showMenuAndTitle: false,
      fontSize: 16
    }
  },
  methods: {
    // 电子书的解析与渲染
    showEpub () {
      // 生成Book对象
      this.book = ePub(DOWNLOAD_URL)
      // console.log(this.book)
      // 通过Book对象生成Rendition对象
      this.rendition = this.book.renderTo('reader', {
        width: window.innerWidth,
        height: window.innerHeight
      })
      // 通过Rendition.display渲染对象
      this.rendition.display()
      // 获取Theme对象
      this.themes = this.rendition.themes
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
      if (!this.showMenuAndTitle) {
        this.$refs.hideSetting.hideSettingBar()
      }
    },
    addFontSize () {
      if (this.fontSize > this.maxFontSize) return
      this.fontSize += 2
      if (this.themes) {
        this.themes.fontSize(this.fontSize + 'px')
      }
    },
    minusFontSize () {
      if (this.fontSize < this.minusFontSize) return
      this.fontSize -= 2
      if (this.themes) {
        this.themes.fontSize(this.fontSize + 'px')
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
