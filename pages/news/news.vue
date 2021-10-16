<template>
	<view>
		<!--自定义头部-->
		<uni-nav-bar :statusBar="true">
			<!--标题左侧-->
			<view class="title-left" slot="left" @tap="jumpPage(0)">
				<view class="iconfont icon-qiandao"></view>
			</view>
			<!--标题中间区域-->
			<view class="title-middle">
				<view class="title-tab" v-for="(item,index) in tab" :key="index"
					@tap="activeHandle(index)"
					:class="index == activeIndex? 'active':''">
					{{item.name}}
				</view>
			</view>
			<!--标题右侧区域-->
			<view class="title-right" slot="right" @tap="jumpPage(1)">
				<view class="iconfont icon-bianji1"></view>
			</view>
		</uni-nav-bar>
		
		<!--页面主内容区域-->
		<swiper :current="activeIndex" :style="{height: swiperHeight + 'px'}" @change="indexChange">
			
			<swiper-item v-if="true" key="0">
				<scroll-view scroll-y="true" style="height: 100%;">
					<FocusPage/>
				</scroll-view>
			</swiper-item>
			
			<swiper-item v-if="true" key="1">
				<scroll-view scroll-y="true" style="height: 100%;">
					<TopicPage/>
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
	import uniNavBar from "../../component/common/navbar/uni-nav-bar.vue"
	import Nothing from "../../component/common/nothing.vue"
	import FocusPage from "../../component/news/focusPage.vue"
	import TopicPage from "../../component/news/topicPage.vue"
	export default {
		components: {
			uniNavBar,
			Nothing,
			FocusPage,
			TopicPage
		},
		onLoad() {
			// 需要动态获取屏幕的高度然后赋值给swiper不然不会生效
			uni.getSystemInfo({
				success: (res) => {
					// console.log(res.windowHeight);
					this.swiperHeight = res.windowHeight - 44;
				}
			});
		},
		data() {
			return {
				tab: [ // 头部tab内容
					{
						name: "关注",
						index: 0
					},
					{
						name: "话题",
						index: 1
					}
				],
				activeIndex: 0, // 选中的Index
				swiperHeight: 0  // 主显示区高度
			}
		},
		methods: {
			// 切换tab选项卡函数
			activeHandle: function(index) {
				this.activeIndex = index;
			},
			
			// 页面跳转函数
			jumpPage: function(type) {
				switch(type) {
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
			
			// 页面向右滑触发的事件
			indexChange: function(e) {
				this.activeIndex = e.detail.current;
				// console.log(this.currentIndex);
			}
		}
	}
</script>

<style lang="scss" scoped>
	.title-left,
	.title-right {
		.iconfont {
			font-size: 40upx;
		}
	}

	.title-right {
		height: 100%;
		width: 80upx;
		text-align: right;

		.iconfont {
			color: #2b2b2b;
		}
	}

	.title-left {
		padding-left: 20upx;

		.iconfont {
			color: #ffa73f;
		}
	}

	.title-middle {
		margin: 0 auto;
		display: flex;
		flex-direction: row;

		.title-tab {
			padding: 0 14upx 0 14upx;
			font-weight: bold;
		}

		.active {
			position: relative;

			&::after {
				position: absolute;
				content: '';
				width: 90%;
				height: 10upx;
				background-color: #fede33;
				bottom: 16upx;
				left: 50%;
				transform: translateX(-50%);
				border-radius: 8upx;
			}
		}
	}
</style>
