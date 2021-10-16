<template>
	<view>
		<!--头部滚动导航栏-->
		<ScrollBar :pageIndex="currentIndex" :nameList="nameList" @changeIndex="activeIndex" />

		<!--主内容-->
		<swiper :current="currentIndex" :style="{height: swiperHeight + 'px'}" @change="indexChange">
			
			<swiper-item v-if="true" v-for="(page,pageIndex) in nameList" :key="pageIndex">
				<scroll-view scroll-y="true" style="height: 100%;" @scrolltolower="loadMore">

					<!--封装好的列表里的子元素组件-->
					<ListItem />
					<ListItem />
					<ListItem />
					<ListItem />
					<ListItem />

				</scroll-view>
			</swiper-item>

			<!--列表为空时显示的样式-->
			<swiper-item v-else>
				<Nothing/>
			</swiper-item>

		</swiper>

	</view>
</template>

<script>
	import ListItem from "../../component/index/listItem.vue"
	import ScrollBar from "../../component/common/scrollBar.vue"
	import Nothing from "../../component/common/nothing.vue"
	export default {
		components: {
			ListItem,
			ScrollBar,
			Nothing
		},
		// 顶部搜索框点击跳转事件
		onNavigationBarSearchInputClicked() {
			uni.navigateTo({
				url:"../search/search"
			})
		},
		// 导航栏头部两个按钮的点击事件
		onNavigationBarButtonTap(e) {
			switch(e.index) {
				case 0: 
					break;
				case 1:
					// 跳转发布动态页面
					uni.navigateTo({
						url:'../publish/publish'
					})
					break;
			}
		},
		data() {
			return {
				swiperHeight: 0, // swiper纵向滚动区域的屏幕高度
				currentIndex: 0, // 滑动页面所在页面的索引值
				nameList: [{ // 头部tab导航栏对应的页面
					name: '关注',
					id: 'guanzhu'
				}, {
					name: '推荐',
					id: 'tuijian'
				}, {
					name: '体育',
					id: 'tiyu'
				}, {
					name: '热点',
					id: 'redian'
				}, {
					name: '财经',
					id: 'caijing'
				}]
			}
		},
		onLoad() {
			// 需要动态获取屏幕的高度然后赋值给swiper不然不会生效
			uni.getSystemInfo({
				success: (res) => {
					// console.log(res.windowHeight);
					this.swiperHeight = res.windowHeight - 55;
				}
			});
		},
		methods: {
			// 页面向右滑触发的事件
			indexChange: function(e) {
				this.currentIndex = e.detail.current;
				// console.log(this.currentIndex);
			},

			// 顶部tab点击触发切换页面事件
			activeIndex: function(index) {
				// console.log(index);
				this.currentIndex = index;
			},

			// 滚动到最底部触发的加载更多事件
			loadMore: function() {
				console.log("加载更多");
			}

		}
	}
</script>

<style lang="scss" scoped>
	
</style>
