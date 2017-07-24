<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <router-link class="tab-item" to="/goods" >商品</router-link>
      <router-link class="tab-item" to="/ratings">评论</router-link>
      <router-link class="tab-item" to="/seller">商家</router-link>
    </div>
    <router-view></router-view>
  </div>
</template>
<script type="text/ecmascript-6">
import header from './components/header/header.vue';
const ERR_OK = 0
export default{
  name: 'app',
  data() {
    return {
      seller: {}
    }
  },
  created () {
    this.$http.get('/api/seller').then((response) => {
      response = response.body
      if (response.errno === ERR_OK) {
        this.seller = response.data;
      }
    })
  },
  components: {
    vHeader: header
  }
}
</script>
<style lang="stylus" type="text/stylus" rel="stylesheet/stylus">
  @import './common/stylus/mixin.styl'
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
  #app
   .tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    border-1px(rgba(7,17,27,0.1))
    .tab-item
      flex: 1
      text-align: center
      display: block
      color:rgb(77,85,92)
      &.active
        color:rgb(240,20,20)


</style>
