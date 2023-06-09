<!--
 * @Author: litao 2412777276@qq.com
 * @Date: 2023-05-22 09:29:51
 * @LastEditors: litao 2412777276@qq.com
 * @LastEditTime: 2023-06-09 16:04:32
 * @FilePath: \vue-product\src\views\home\index.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template> 
  <div class="home">
    <div class="home-header">
      <div class="home-search">
        <svg-icon icon-class="search" class="search-icon"></svg-icon>
        <router-link tag="span" to="/search" class="search-title">推荐搜索 关键词</router-link>
      </div>
      <svg-icon icon-class="customer-service"></svg-icon>
    </div>
    <van-swipe
      lazy-render
      :autoplay="3000"
      :show-indicators="false"
      >
       <van-swipe-item
        v-for="(item, index) in bannerImages"
        :key="index"
        >
        <img :src="item.imgUrl" @click="handleClick">
      </van-swipe-item>
    </van-swipe>
    <div class="home-tags">
      <ul class="tag-content">
        <template v-for="(item,index) in tagList" :key="index">
          <router-link :to="item.url" tag="li" class="tag-item">
            <svg-icon :icon-class="item.iconName"></svg-icon>
            <span class="tag-name">{{item.tagName}}</span>
          </router-link>
        </template>
      </ul>
    </div>
    <section class="spike-area">
      <ul class="spike-top">
        <router-link tag="li" class="top-left" to="/chainCatSpike">
          <div class="item-top">
            <span class="top-title">链猫秒杀</span>
            <div class="count-down">
              <span class="count-title">14点场</span>
              <van-count-down :time="time">
              </van-count-down>
            </div> 
          </div>
          <div class="item-info">
            <div class="item-content">
              <img src="../../assets/image/home/demo1.png"/>
              <span class="price">￥298</span>
              <span class="old-price">￥399</span>
            </div>
            <div class="item-content">
              <img src="../../assets/image/home/demo2.png"/>
              <span class="price">￥298</span>
              <span class="old-price">￥399</span>
            </div>
            <div class="item-content">
              <img src="../../assets/image/home/demo3.png"/>
              <span class="price">￥298</span>
              <span class="old-price">￥399</span>
            </div>
          </div>
        </router-link>
        <router-link tag="li" class="top-right" to="/foundGoodGoods">
          <div class="item-top">
            <span class="top-title">发现好货</span>
            <span class="good-tag">品质好物</span>
          </div>
          <div class="item-info">
            <div class="item-content">
              <span class="cheap">好物不贵</span>
              <img src="../../assets/image/home/demo4.png">
            </div>
            <div class="item-content">
              <img src="../../assets/image/home/demo5.png">
            </div>
          </div>
        </router-link>
      </ul>
      <ul class="spike-center">
        <router-link tag="li" to="/specialSpike" class="center-item">
            <span class="item-title">特价秒杀</span>
            <span class="special-desc" style="color:#ff9351">10元抢购</span>
            <img src="../../assets/image/home/demo6.png">
        </router-link>
        <router-link tag="li" to="/brandSpike" class="center-item">
            <span class="item-title">品牌秒杀</span>
            <span class="brand-desc" style="color: rgb(221, 55, 73)">笔记本秒杀</span>
            <img src="../../assets/image/home/demo7.png">
        </router-link>
        <router-link tag="li" to="/newProductLaunch" class="center-item">
            <span class="item-title">新品首发</span>
            <span class="pro-desc" style="color: #ff9351;">小黑盒新品</span>
            <img src="../../assets/image/home/demo8.png">
        </router-link>
        <router-link tag="li" to="/premiumRanking" class="center-item">
            <span class="item-title">优品排行</span>
            <span class="rank-desc" style="color: rgb(145, 201, 91);">榜上好物购</span>
            <img src="../../assets/image/home/demo9.png">
        </router-link>
      </ul>
      <ul class="spike-bottom">
        <router-link tag="li" class="bottom-left" to="/foundGoodGoods">
          <div class="item-top">
            <span class="top-title">大牌购走</span>
            <span class="good-tag">
              戴尔
              <svg-icon icon-class="right-arrow" class="right-arrow"></svg-icon>
            </span>
          </div>
          <div class="item-info">
            <div class="item-content">
              <span class="img-title">信赖大品牌</span>
              <img src="../../assets/image/home/demo10.png">
            </div>
            <div class="item-content">
              <img src="../../assets/image/home/demo11.png">
            </div>
          </div>
        </router-link>
        <router-link tag="li" class="bottom-right" to="/loveShop">
          <div class="item-top">
            <span class="top-title">爱逛好店</span>
            <span class="good-tag">懂你所要</span>
          </div>
          <div class="item-info">
            <div class="item-content">
              <span class="img-title">来逛个够</span>
              <img src="../../assets/image/home/demo12.png">
            </div>
            <div class="item-content">
              <img src="../../assets/image/home/demo13.png">
            </div>
          </div>
        </router-link>
      </ul>
    </section>
    <div class="content-tabs">
      <van-tabs
        title-active-color="#D8182D"
        title-inactive-color="#3a3a3a"
        background="transparent"
        v-model:active="active"
        :swipe-threshold="5"
      >
        <van-tab
          v-for="(tab, index) in tabList"
          :key="index"
          :title="tab.describe"
          :name="tab.type">
          <template #title>
            <div class="slot-title">  
              <b class="tab-title">{{tab.title}}</b>
              <span class="tab-name">{{tab.name}}</span>
            </div>
          </template>
          <section class="goods-box">
            <ul class="goods-content">
              <li v-for="(item,index) in tab.list" :key="index">
                <router-link tag="div" to="/classify/product" class="goods-thing">
                  <img :src="item.img">
                </router-link>
                <div class="goods-info">
                  <span class="goods-title">{{item.title}}</span>
                  <div class="goods-cart">
                    <span class="cart-left">{{item.forceValue}}倍算力</span>
                    <i class="cart-right">
                      <svg-icon icon-class="add" @click="addCart"></svg-icon>
                    </i>
                  </div>
              </div>
              </li>
            </ul>
          </section>
        </van-tab>
      </van-tabs>
    </div>
  </div>
</template>

<script>
import { ref, reactive, toRefs, getCurrentInstance, toRaw } from "vue";
export default {
  setup () {
    const {proxy} = getCurrentInstance()
    const searchText = ref('')
    const state = reactive({
      bannerImages: [],
      tabList: []
    })
    const tagList = reactive([
      {
        iconName: 'chain-cat-boutique',
        tagName: '链猫精品',
        url: './search'
      },
      {
        iconName: 'cm-area',
        tagName: 'CM专区',
        url: './search'
      },
      {
        iconName: 'collar-cm',
        tagName: '领CM币',
        url: './search'
      },
      {
        iconName: 'coupon-svg',
        tagName: '领券',
        url: './search'
      },
      {
        iconName: 'chain-cat-member',
        tagName: '链猫会员',
        url: './search'
      }
    ])
    const endTime = '2023-05-26 16:20:00'
    const time = ref(new Date(endTime).getTime() - Date.now())
    proxy.$http.get('http://test.happymmall.com/home/homeData').then(res => {
      const {images, tabList} = res.data
      state.bannerImages = images
      state.tabList = tabList
    })
    const addCart = el => {
      
    }
    return {
      ...toRefs(state),
      tagList,
      time
    }
  },
  
}
</script>

<style lang="scss" src="./index.scss">

</style>

