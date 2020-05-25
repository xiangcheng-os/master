<template>
  <div class="detail-swiper">
    <swiper>
      <swiper-item class="image-height" v-for="item in topImages" :key="item.index">
        <img :src="item" alt="">
      </swiper-item>
    </swiper>
  </div>

  
</template>

<script>
import {Swiper,SwiperItem} from 'components/common/swiper'
export default {
  name:"DetailSwiper",
  components:{
    Swiper,
    SwiperItem
  },
  props: {
    topImages: {
      type:Array,
      default() {
        return[]
      }
    }
  }

}
</script>

<style>
.image-height{
  height: 300px;
}

</style>