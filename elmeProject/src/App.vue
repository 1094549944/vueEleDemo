<template>
  <div id="app">
    <header-bar :seller="seller"></header-bar>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link tag="a"
                     to='/goods'>
          商品
        </router-link>
      </div>
      <div class="tab-item">
        <router-link to='/ratings'
                     tag="a">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to='seller'
                     tag="a">商家</router-link>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
import axios from 'axios'
import headerBar from '@/components/header'
export default {
  name: 'App',
  components: {
    headerBar
  },
  data () {
    return {
      seller: {}
    }
  },
  methods: {
    getSellerData () {
      axios.get('/api/seller.json', {
        params: {
          id: '1'
        }
      }).then(this.handleGetData)
    },
    handleGetData (res) {
      res = res.data

      this.seller = res.seller
      console.log(this.seller)
    }
  },
  created () {
    this.getSellerData()
  }
}
</script>

<style lang="stylus">
@import './common/stylus/mixin.styl'

.tab
  display flex
  width 100%
  height 40px
  line-height 40px
  border-1px(rgba(7, 17, 27, 0.1))

  .tab-item
    flex 1
    text-align center

    a
      display block
      font-size 14px
      color rgb(77, 85, 93)
      text-decoration none

    .router-link-active
      color rgb(240, 20, 20)
      text-decoration none
</style>
