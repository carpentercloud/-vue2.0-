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
    <transition name="fade">
      <div v-if="detailStatus" class="seller-detail">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>
            <star :size="48" :score="4.5"></star>
            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <ul v-if="seller.supports" class="supports">
              <li class="supports-item" v-for="(item, index) in seller.supports">
                <span class="icon" :class="classMap[item.type]"></span>
                <span class="text">{{item.description}}</span>
              </li>
            </ul>
            <div class="title">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>
            <div class="bulletin">
              <p class="content">{{seller.bulletin}}</p>
            </div>
          </div>
        </div>
        <div class="detail-close" @click="hideDetail">
          <i class="icon-close"></i>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import star from 'components/star/star.vue'
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
  },
  components: {
    star
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
    &.fade-enter-active, &.fade-leave-active {
      transition: all 0.5s;
    }
    &.fade-enter, &.fade-leave-active {
      opacity: 0;
      background: rgba(7, 17, 27, 0)
    }
    .detail-wrapper {
      width: 100%;
      min-height: 100%;
      .detail-main {
        padding-bottom: 64px;
        width: 80%;
        margin: 60px auto 0;
        text-align: center;
        .name {
          font-size: 16px;
          font-weight: 700;
          margin-bottom: 16px;
        }
        .title {
          display: flex;
          margin: 28px auto 24px auto;
          .line {
            position: relative;
            flex: 1;
            top: -6px;
            border-bottom: 1px solid rgba(255,255,255,0.2);
          }
          .text {
            padding: 0 12px;
            font-size: 14px;
            font-weight: 700;
          }
        }
        .supports {
          margin: 0 auto;
          text-align: left;
          font-size: 0px;
          .supports-item {
            padding: 0 12px;
            margin-bottom: 12px;
            .icon {
              display: inline-block;
              width: 16px;
              height: 16px;
              margin-right: 6px;
              vertical-align: top;
              background-size: 16px 16px;
              background-repeat: no-repeat;
              &.decrease {
                bg-image('decrease_2');
              }
              &.discount {
                bg-image('discount_2');
              }
              &.guarantee {
                bg-image('guarantee_2');
              }
              &.invoice {
                bg-image('invoice_2');
              }
              &.special {
                bg-image('special_2');
              }
            }
            .text {
              font-size: 12px;
              line-height: 16px;
            }
          }
        }
        .bulletin {
          .content {
            font-size: 12px;
            line-height: 24px;
            text-align: left;
          }
        }
      }
    }
    .detail-close {
      position: relative;
      height: 32px;
      width: 32px;
      margin: -64px auto 0 auto;
      line-height: 64px;
      clear: both;
      font-size: 32px;
    }
  }
}
</style>
