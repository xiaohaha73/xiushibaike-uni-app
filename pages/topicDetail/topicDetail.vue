<template>
	<view>
		<view class="themeImg">
			<image src="../../static/demo/topicpic/12.jpeg"></image>
		</view>
		<view class="header">
			<view class="top">
				<image src="../../static/demo/topicpic/12.jpeg" mode="widthFix"></image>
				<view class="name">
					#忆往事,敬余生#
				</view>
			</view>
			<view class="center">
				动态 793 今日 641
			</view>
			<view class="bottom">
				弱小和无知不是生存的障碍，傲慢才是
			</view>
		</view>
		<view class="tab">
			<view class="tab-name" @tap="currentHandle(0)" :class="currentIndex === 0? 'active':''">
				默认
			</view>
			<view class="tab-name" @tap="currentHandle(1)" :class="currentIndex === 1? 'active':''">
				最新
			</view>
		</view>
		
		<view class="main">
			<!--主内容-->
			<swiper :current="currentIndex" :style="{height: swiperHeight + 'px'}" @change="indexChange">
				
				<swiper-item v-if="true" key="0">
					<scroll-view scroll-y="true" style="height: 100%;" @scrolltolower="loadMore">
						<ListItem/>
						<ListItem/>
						<ListItem/>
						<ListItem/>
						<ListItem/>
						<ListItem/>
					</scroll-view>
				</swiper-item>
				
				<swiper-item v-if="true" key="1">
					<scroll-view scroll-y="true" style="height: 100%;" @scrolltolower="loadMore">
						<ListItem/>
						<ListItem/>
						<ListItem/>
						<ListItem/>
						<ListItem/>
						<ListItem/>
					</scroll-view>
				</swiper-item>
			
				<!--列表为空时显示的样式-->
				<swiper-item v-else>
					<Nothing/>
				</swiper-item>
			
			</swiper>
		</view>
	</view>
</template>

<script>
	import Nothing from "../../component/common/nothing.vue";
	import ListItem from "../../component/common/listItem.vue";
	export default {
		components:{
			Nothing,
			ListItem
		},
		data() {
			return {
				swiperHeight: 0, // 滑动区域的高度
				currentIndex: 0 // 选中的tab索引值
			}
		},
		onLoad() {
			// 需要动态获取屏幕的高度然后赋值给swiper不然不会生效
			uni.getSystemInfo({
				success: (res) => {
					// console.log(res.windowHeight);
					this.swiperHeight = res.windowHeight - 305;
				}
			});
		},
		// 下拉刷新事件
		onPullDownRefresh() {
			
			setTimeout(function(){
				// 关闭下拉刷新
				uni.stopPullDownRefresh();
			},4000); 
			
		},
		methods: {
			currentHandle: function(index){
				this.currentIndex = index;
			},
			indexChange: function(e) {
				this.currentIndex = e.detail.current;
				// console.log(this.currentIndex);
			},
			// 加载更多
			loadMore: function() {
				console.log("加载更多");
			}
		}
	}
</script>

<style lang="scss" scoped>
.themeImg {
	width: 100%;
	height: 300upx;
	overflow: hidden;
	image {
		width: 100%;
		height: 100%;
		filter: blur(12upx);
	}
}

.header {
	padding: 20upx;
	.top {
		position: relative;
		image {
			width: 150upx;
			height: 150upx;
			border-radius: 20upx;
			position: absolute;
			// left: 5px;
			top: -48px;
		}
		.name {
			margin-left: 176upx;
			font-weight: bold;
		}
	}
	.center {
		margin-top: 30upx;
		color: #d5d5d5;
		font-size: 26upx;
	}
	.bottom {
		margin-top: 28upx;
		color: #9b9b9b;
		font-size: 28upx;
	}
}

.tab {
	display: flex;
	flex-direction: row;
	padding: 20upx 0 40upx 0;
	.tab-name {
		flex: 1;
		text-align: center;
		font-size: 28upx;
		color: #979797;
		font-weight: bold;
	}
	
	.active {
		color: #313131;
		position: relative;
		&::after {
			content: '';
			height: 8upx;
			width: 68upx;
			background-color: #fede33;
			position: absolute;
			transform: translateX(-50%);
			left: 50%;
			bottom: -4upx;
			border-radius: 8upx;
		}
	}
}

.main {
	
}
</style>
