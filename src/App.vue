<template>
  <div id="app">   
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/" active-class="active">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings" active-class="active">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller" active-class="active">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import header from 'components/header/header.vue'

const ERR_OK = 0
export default {
  data () {
    return {
      seller: {}
    }
  },
  created () {
    this.$http.get('/api/seller').then((response) => {
      response = response.body
      if (response.errno === ERR_OK) {
        this.seller = response.data
      }
    })
  },
  components: {
    'v-header': header
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import 'common/stylus/mixin'
#app {
  .tab {
    width: 100%;
    height: 40px;
    line-height 40px;
    display: flex;
    flex: 1;
    border-1px(rgba(7, 17, 27, 0.1))
    .tab-item {
      flex: 1;
      text-align:  center;
      a {
        display: block;
        font-size: 14px;
        color: rgb(77,85,93);
        &.active {
          color: rgb(240,20,20)
        }
      }
    }
  }
}
</style>
