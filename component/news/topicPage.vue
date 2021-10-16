<template>
	<scroll-view scroll-y="true" style="height: 100%;" @scrolltolower="loadMore">
		<!--搜索框-->
		<view class="search-bar">
			<input type="text" placeholder="搜索内容" placeholder-class="placeholder iconfont icon-sousuo"/>
		</view>
		<!--轮播图-->
		<swiper class="swiperBanner" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" :circular="true">
			<swiper-item>
				<image src="../../static/demo/banner1.jpg" lazy-load></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/demo/banner2.jpg" lazy-load></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/demo/banner3.jpg" lazy-load></image>
			</swiper-item>
		</swiper>
		<!--热门分类-->
		<HotCate :tags="tags"/>
		<!--最近更新-->
		<view class="news-list">
			<view class="news-title">
				最近更新
			</view>
			<NewsItem/>
			<NewsItem/>
			<NewsItem/>
			<NewsItem/>
		</view>
		
	</scroll-view>
</template>

<script>
	import HotCate from "./hotcategrory.vue"
	import NewsItem from "./newsItem.vue"
	export default {
		components: {
			HotCate,
			NewsItem
		},
		data() {
			return {
				// 热门分类标签tag
				tags: [
					{name:'最新'},
					{name:'游戏'},
					{name:'情感'},
					{name:'打卡'},
					{name:'故事'},
					{name:'喜爱'},
				]
				
			}
		},
		methods: {
			loadMore: function() {
				console.log("加载更多");
			}
		}
	}
</script>

<style lang="scss" scoped>
	
	.search-bar {
		padding: 20upx;
		> input {
			background-color: #f4f4f4;
			height: 66upx;
			border-radius: 10upx;
			padding-left: 20upx;
		}
		.placeholder {
			display: flex;
			flex-direction: row;
			justify-content: center;
			font-size: 26upx;
		}
	}
	.swiperBanner {
		padding: 0 20upx 14upx 20upx;
		height: 21%;
		border-bottom: 4upx solid #f4f4f4;
		
		swiper-item {
			width: 100%;
			height: 100%;
		}
		image {
			height: 100%;
			width: 100%;
			
		}
	}
	
	.news-list {
		padding: 20upx;
		.news-title{
			font-size: 26upx;
			margin-bottom: 25upx;
		}
	}
	
</style>
