<template>
  <view class="swiper-item-2" v-if="swiperModel.swiperList">
    <view class="swiper-bgColor" :style="{background: swiperBgColor}"></view>
    <view class="swiper-head">
      <swiper-search></swiper-search>
    </view>
    <view class="swiper-cont">
      <swiper :autoplay="true" @change="changeSwiper" :circular="true" :indicator-dots="true" indicator-active-color="#c91230" indicator-color="#ebedf0" :style="{ height: swiperHeight + 'px' }">
        <swiper-item v-for="(item, index) in swiperModel.swiperList" :key="index">
          <view :title="item.name" @click="goLinks(item.url.value)">
            <img :src="item.image" :alt="item.intro" :style="{ height: swiperHeight + 'px' }" class="bgImg" />
          </view>
        </swiper-item>
      </swiper>
    </view>

  </view>
</template>
<script>
  import swiperSearch from './swiper-search'
  import mxins from './mixins'
  export default {
    mixins: [mxins],
    components: { swiperSearch },
    data () {
      return {
        async: false,
        widgetModel: '',
        swiperHeight: 150,
        windowWidth: '',
        swiperBgColor: '#421f7d',
        swiperList: []
      }
    },
    props: {
      swiperModel: {},
      height: {
        type: Number,
        default: 150
      }
    },
    mounted () {
      this.init()
    },
    methods: {
      init () {
        var para = {
          detail: {
            current: 0
          }
        }
        this.changeSwiper(para)
      },
      goLinks (url) {
        this.$api.to(url)
      },
      changeSwiper (ev) {
        this.swiperBgColor = this.swiperModel.swiperList[ev.detail.current].colors
      }
    },
    watch: {
      widget: 'watchWidget'
    }
  }
</script>
<style lang="scss" scoped>
  @import "@/assets/style/variable.scss";

  .swiper-item-2 {
    position: relative;
    .swiper-bgColor {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 180px;
      background: #421f7d;
      border-radius: 0 0 15px 15px;
    }
    .swiper-head {
      width: 100%;
      position: relative;
      height: 45px;
    }
    .swiper-cont {
      padding: 0 10px;
      .uni-swiper-item {
        padding-top: 0px !important;
      }
      .uni-swiper {
        height: 180px;
      }
      .uni-swiper .uni-swiper-dot {
        width: 6px;
        height: 6px;
      }
      .bgImg {
        width: 100%;
        border-radius: 10px;
      }
    }
  }
</style>
