title: vue轮播插件的快速使用
author: suijiafeng
tags: []
categories: []
date: 2018-04-30 10:56:00
---

Vue-Awesome-Swiper 基于 Swiper4、适用于 Vue 的轮播组件，支持服务端渲染和单页应用。


如果需要回退到 Swiper3，请使用 v2.6.7 版本
跟着下面的步骤，一起构建一个轮播图组件吧。

 1、使用NPM下载依赖包

		npm install vue-awesome-swiper --save

2、全局注册

		import Vue from 'vue'
		import VueAwesomeSwiper from 'vue-awesome-swiper'
		 
		// require styles
		import 'swiper/dist/css/swiper.css'
		 
		Vue.use(VueAwesomeSwiper, /* { default global options } */)

3、复制插件的通用模板

		<!-- The ref attr used to find the swiper instance -->
		<template>
		  <swiper :options="swiperOption" ref="mySwiper" @someSwiperEvent="callback">
		    <!-- slides -->
		    <swiper-slide>I'm Slide 1</swiper-slide>
		    <swiper-slide>I'm Slide 2</swiper-slide>
		    <swiper-slide>I'm Slide 3</swiper-slide>
		    <swiper-slide>I'm Slide 4</swiper-slide>
		    <swiper-slide>I'm Slide 5</swiper-slide>
		    <swiper-slide>I'm Slide 6</swiper-slide>
		    <swiper-slide>I'm Slide 7</swiper-slide>
		    <!-- Optional controls -->
		    <div class="swiper-pagination"  slot="pagination"></div>
		    <div class="swiper-button-prev" slot="button-prev"></div>
		    <div class="swiper-button-next" slot="button-next"></div>
		    <div class="swiper-scrollbar"   slot="scrollbar"></div>
		  </swiper>
		</template>
		 
		<script>
		  export default {
		    name: 'carrousel',
		    data() {
		      return {
		        swiperOption: {
          loop:true,
          pagination:{
            el:".swiper-pagination",
            clickable:true
          }
		          // some swiper options/callbacks
		          // 所有的参数同 swiper 官方 api 参数
		          // ...
		        }
		      }
		    },
		    computed: {
		      swiper() {
		        return this.$refs.mySwiper.swiper
		      }
		    },
		    mounted() {
		      // current swiper instance
		      // 然后你就可以使用当前上下文内的swiper对象去做你想做的事了
		      console.log('this is current swiper instance object', this.swiper)
		      this.swiper.slideTo(3, 1000, false)
		    }
		  }
		</script>

4、根据实际需要，设置轮播图参数，例如，自动轮播，分页器，左右切换控制箭头，滚动速度等；
相关配置详情请上 [swiper](http://www.swiper.com.cn/api/index2.html)官网