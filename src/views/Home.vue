<template>
  <div class='home'>
    <vue-kline :klineParams='klineParams' :klineData='klineData' ref='callMethods'></vue-kline>
    <div id="sidebarTheme">
      <div class="sidebar">
        <ul>
          <li @click="flag=false"><span class="icon iconfont klineguanji"></span></li>
          <li @click="flag=1"><span class="icon iconfont klinewendang"></span></li>
          <li @click="flag=2"><span class="icon iconfont klineclock"></span></li>
          <li @click="flag=3"><span class="icon iconfont klinefire"></span></li>
          <li @click="flag=4"><span class="icon iconfont klineDate"></span></li>
          <li @click="flag=5"><span class="icon iconfont klinemessage"></span></li>
          <li @click="flag=6"><span class="icon iconfont klinelight"></span></li>
        </ul>
      </div>
      <div class="content" v-show="flag==1">
        <div class="contentTitle">数据窗口</div>
      </div>
      <div class="content" v-show="flag==2">
        <div class="contentTitle">管理警报</div>
      </div>
      <div class="content" v-show="flag==3">
        <div class="contentTitle">成交量</div>
      </div>
      <div class="content" v-show="flag==4">
        <div class="contentTitle">财经日历</div>
      </div>
      <div class="content" v-show="flag==5">
        <div class="contentTitle">新闻</div>
      </div>
      <div class="content" v-show="flag==6">
        <div class="contentTitle">LWSB</div>
      </div>
    </div>
  </div>
</template>

<script>
import vueKline from 'vue-kline'
import data from '@/assets/data'
export default {
  name: 'home',
  data () {
    return {
      flag: false,
      screenWidth: document.body.clientWidth,
      screenHeight: document.body.clientWidth,
      klineParams: {
        width: document.body.clientWidth - 50,
        height: document.body.clientHeight,
        theme: 'light',
        language: 'zh-cn',
        ranges: ['1w', '1d', '1h', '30m', '15m', '5m', '1m', 'line'],
        symbol: 'BTC',
        symbolName: 'BTC/USD',
        intervalTime: 5000,
        depthWidth: 50
      },
      klineData: data
    }
  },
  watch: {
    flag (val) {
      val !== false ? this.$refs.callMethods.resize(this.screenWidth - 50 - 280, this.screenHeight) : this.$refs.callMethods.resize(this.screenWidth - 50, this.screenHeight)
    }
  },
  components: {
    vueKline
  },
  methods: {
    handle () {
      this.flag = !this.flag
      this.$refs.callMethods.resize(this.screenWidth - 50 - 280, this.screenHeight)
    }
  },
  mounted () {
    this.screenWidth = document.body.clientWidth
    this.screenHeight = document.body.clientHeight
    let that = this
    window.onresize = () => {
      return (() => {
        this.screenWidth = document.body.clientWidth
        this.screenHeight = document.body.clientHeight
        that.flag !== false ? this.$refs.callMethods.resize(this.screenWidth - 50 - 280, this.screenHeight) : this.$refs.callMethods.resize(this.screenWidth - 50, this.screenHeight)
        // that.$refs.callMethods.resize(this.screenWidth - 50, this.screenHeight)
      })()
    }
  }
}
</script>
<style lang='less'>
html,
body {
  height: 100%;
}
.home{
  .sidebar{
    position: absolute;
    top: 0;
    right: 0;
    width: 50px;
    z-index: 999;
    height: 100%;
    border-left: 1px solid #ccc;
    ul{
      list-style: none;
      margin: 0;
      cursor: pointer;
      padding: 4px;
      box-sizing: border-box;
      li{
        width: 40px;
        height: 40px;
        line-height: 40px;
        margin-top: 10px;
        .icon{
          font-size: 22px;
        }
      }
      li:hover{
        background-color: #eee;
        border-radius: 5px;
      }
    }
  }
  .content{
    width: 280px;
    height: 100%;
    position: absolute;
    top: 0;
    right: 51px;
    z-index: 999;
    border-left: 1px solid #ccc;
    padding: 2px;
    box-sizing: border-box;
    .contentTitle{
      width: 100%;
      height: 35px;
      line-height: 35px;
      border-radius: 2px;
      font-size: 14px;
      text-align: left;
      padding-left: 10px;
      box-sizing: border-box;
    }
  }
}
.light{
  .sidebar{
    background-color: #fff;
    border-left: 1px solid #ccc;
    ul li .icon{
      color: #333;
    }
    ul li:hover{
      background-color: #eee;
    }
  }
  .content{
    background-color: #fff;
    .contentTitle{
      background-color: #eee;
      color:#000;
    }
  }
}
.dark{
  .sidebar{
    background-color: #131722;
    border-left: 1px solid #404040;
    ul li .icon{
      color: #72757F;
    }
    ul li:hover{
      background-color: #2A2E39;
    }
  }
  .content{
    background-color: #131722;
    border-left: 1px solid #404040;
    .contentTitle{
      background-color: #262B3E;
      color:#fff;
    }
  }
}
</style>
