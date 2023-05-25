<!--
 * @Author: litao 2412777276@qq.com
 * @Date: 2023-05-22 09:29:51
 * @LastEditors: litao 2412777276@qq.com
 * @LastEditTime: 2023-05-25 17:19:32
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
        </router-link>
      </ul>
      <ul class="spike-center"></ul>
      <ul class="spike-bottom"></ul>
    </section>
  </div>
</template>

<script>
import { ref, reactive, toRefs, getCurrentInstance, toRaw } from "vue";
export default {
  setup () {
    const {proxy} = getCurrentInstance()
    const searchText = ref('')
    const state = reactive({
      bannerImages: []
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
      const {images} = res.data
      state.bannerImages = images
    })
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

