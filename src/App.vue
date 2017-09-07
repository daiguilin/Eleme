<template>
  <div>
    <v-header :seller="selldata"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <a href="#" v-link="{path:'/goods'}">商品</a>
      </div>
      <div class="tab-item">
         <a href="#" v-link="{path:'/ratings'}">评论</a>
      </div>
      <div class="tab-item">
         <a href="#" v-link="{path:'/seller'}">商家</a>
      </div>
    </div>
    <router-view :seller="selldata" keep-alive> </router-view> 
  </div>            
</template>
<script>
import {urlParse} from '././common/js/util.js'
import header from './components/header/header.vue'
const ERR_OK = 0
export default {
    data() {
      return {
        selldata: {
          /*id: (() => {
            let queryParam = urlParse();
            console.log(queryParam)
            return queryParam.id;
          })()*/
        }
      }
    },
    created() {
      this.$http.get('/api/seller').then((response) => {
          response=response.body;
          //console.log(response.data)
          if(response.errno === ERR_OK){
              this.selldata=response.data;
              //console.log(this.selldata)
          }
      })
    },
    components: {
      'v-header': header
    } 
  }
</script>
<style lang="stylus">
    @import "./common/stylus/mixin.styl"
    .tab
      display:flex
      width : 100%
      height:40px
      line-height: 40px
      //border-bottom:1px solid rgba(7,17,27,0.1)
      border-1px(rgba(7,17,27,0.1))
      .tab-item
        flex:1
        text-align:center
        & > a
            display:block
            font-size:14px
            color:rgb(77,85,93)
            &.active
                    color:rgb(242,20,20)
  
</style> 