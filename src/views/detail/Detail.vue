
<template>
  <div id="detail">
    <detail-nav-bar class="detail-nav"></detail-nav-bar>
    <scroll class="content">
      <detail-swiper :top-images="topImages"></detail-swiper>
      <detail-base-info :goods="goods"></detail-base-info>
      <detail-shop-info :shop="shop"></detail-shop-info>
      <detail-goods-info :detail-info="detailInfo"></detail-goods-info>
      <dateil-param-info :param-info="paramInfo"></dateil-param-info>
    </scroll>
    
    
  </div>
  
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar'
import DetailSwiper from './childComps/DetailSwiper'
import DetailBaseInfo from "./childComps/DetailBaseInfo"
import DetailShopInfo from "./childComps/DetailShopInfo"
import DetailGoodsInfo from "./childComps/DetailGoodsInfo"
import Scroll from "components/common/scroll/Scroll"
import DetailParamInfo from "./childComps/DetailParamInfo"
import {getDetail,Goods,Shop,GoodsParam} from '../../network/detail'

export default {
  name:"Detail",
  components: {
    DetailNavBar,
    DetailSwiper,
    DetailBaseInfo,
    DetailShopInfo,
    Scroll,
    DetailGoodsInfo,
    DetailParamInfo
  },
  data() {
    return {
      iid:null,
      topImages: [],
      goods:{},
      shop:{},
      detailInfo:{},
      paramInfo:{},
    }
  },
  
  created() {
    //1.保存传入的iid
    this.iid = this.$route.params.iid
    //2根据iid请求详细数据
    getDetail(this.iid).then(res => {
      console.log(res)
      //1.获取顶部的图片轮播数据
      const data = res.result;
      this.topImages = data.itemInfo.topImages

      //2.获取商品信息
      this.goods = new Goods(data.itemInfo,data.columns,data.shopInfo.services)

      //3.创建店铺信息对象
      this.shop = new Shop(data.shopInfo)
      // 4.保存商品的详情数据
      this.detailInfo = data.detailInfo;
      // 5.获取参数的信息
      this.paramInfo = new GoodsParam(data.itemParams.info,data.itemParams.rule)
    })
  }
}
</script>

<style scoped>
#detail {
  position: relative;
  z-index: 9;
  background-color: #fff;
  height: 100vh;
}

.detail-nav {
  position: relative;
  z-index: 9;
  background-color: #fff;
  
}

.content{
  height: calc(100% - 44px);
}
</style>