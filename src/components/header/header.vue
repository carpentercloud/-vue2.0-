<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support" >
          <span class="icon" :class="this.classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="back-img">
      <img :src="seller.avatar" width="100%" height="100%" >
    </div>
    <div v-if="detailStatus" class="seller-detail"></div>
  </div>
</template>

<script>
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      detailStatus: false
    }
  },
  methods: {
    showDetail () {
      this.detailStatus = true
    },
    hideDetail () {
      this.detailStatus = false
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  }
}
</script>
<style lang="stylus" rel="stylesheet/stylus">
@import '../../common/stylus/mixin.styl'
.header {
  background: rgba(7,17,27,0.5);
  color: #fff;
  position: relative;
  .content-wrapper {
    position: relative;
    padding: 24px 12px 18px 24px;
    font-size: 0px;
    .avatar{
      display: inline-block;
      border-radius: 2px;
      vertical-align: top;
    }
    .content {
      display: inline-block;
      margin-left: 16px;
      font-size: 12px;
      .title {
        .brand {
          display: inline-block;
          width: 30px;
          height: 18px;
          vertical-align: top;
          bg-image('brand');
          background-size: 30px 18px;
        }
        .name {
          font-size: 16px;
          font-weight: bold;
          line-height: 18px;
        }
      }
      .description {
        margin: 8px 0px 10px 0px;
        font-size: 12px;
      }
      .support {
        height: 12px;
        .icon {
          display: inline-block;
          width: 12px;
          height: 12px;
          vertical-align: top;
          background-size: 12px;
          margin-right: 4px;
          background-repeat: no-repeat;
          &.decrease {
            bg-image('decrease_1');
          }
          &.discount {
            bg-image('discount_1');
          }
          &.guarantee {
            bg-image('guarantee_1');
          }
          &.incoice {
            bg-image('invoice_1');
          }
          &.special {
            bg-image('special_1');
          }
        }
        .text {
          line-height:12px;
          font-size: 10px;
        }
      }
    }
    .support-count {
      position: absolute;
      right: 12px;
      bottom: 14px;
      padding: 0 8px;
      height: 24px;
      line-height: 24px;
      border-radius: 14px;
      background: rgba(0, 0, 0, 0.2);
      text-align: center;
      .count {
        font-size: 10px;
        vertical-align: top;
      }
      .icon-keyboard_arrow_right {
        margin-left: 2px;
        line-height: 24px;
        font-size: 10px;
      }
    }
  }
  .bulletin-wrapper {
    position: relative;
    padding: 0px 22px 0px 12px;
    height: 28px;
    line-height: 28px;
    background: rgba(7, 17, 27, 0.2)
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    .bulletin-title {
      display: inline-block;
      // vertical-align: top;
      margin-top: 8px;
      width: 22px;
      height: 12px;
      bg-image('bulletin');
      background-size: 22px 12px;
      background-repeat: no-repeat;
    }
    .bulletin-text {
      vertical-align: middle;
      margin: 0px 4px;
      // line-height: 30px;
      font-size: 10px;
    }
    .icon-keyboard_arrow_right {
      position: absolute;
      font-size: 12px
      right: 12px
      top: 8px
    }
  }
  .back-img {
    position: absolute;
    top: 0px;
    left: 0px;
    width:100%;
    height: 100%;
    z-index: -1;
    filter: blur(10px);
  }
  .seller-detail {
    position: fixed;
    top: 0px;
    left: 0px;
    z-index: 100;
    width: 100%;
    height: 100%;
    overflow: auto;
    background: rgba(7, 17, 27, 0.8);
  }
}
</style>
