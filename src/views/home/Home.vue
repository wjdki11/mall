<template>
  <div>
  <nav-bar class="home-nav"><template v-slot:center><div>购物街</div></template></nav-bar>
  <home-swiper :banners="banners"/>
  <recommend-view :recommends="recommends"/>
  <feature-view/>
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar'
import HomeSwiper from 'views/home/childComps/HomeSwiper'
import RecommendView from 'views/home/childComps/RecommendView'
import FeatureView from 'views/home/childComps/FeatureView'
import {getHomeMultidata} from 'network/home'

  export default {
    name: "Home",
    components: {
      NavBar,
      HomeSwiper,
      RecommendView,
      FeatureView
    },
    data() {
      return {
        banners: [],
        recommends: [],
      }
    },
    created() {
      //请求多个数据
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      })
    },
  }

</script>

<style>
.home-nav{
  background-color: var(--color-tint);
  color: #fff;
}
</style>
