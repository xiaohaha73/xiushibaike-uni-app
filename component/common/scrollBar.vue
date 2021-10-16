<template>
	<!--顶部横向滚动导航栏-->
	<view class="uni-tab-bar">
			<scroll-view scroll-x class="uni-swiper-tab">
				<block v-for="(tab,index) in nameList" :key="tab.id">
					<view class="swiper-tab-list" 
					:class="{'active':pageIndex==index}"
					@tap="activeTab(index)">
						{{tab.name}}
					</view>
				</block>
			</scroll-view>
		</view>
</template>

<script>
	export default {
		props: {
			pageIndex: {
				type: Number,
				default:0
			},
			nameList: {
				type: Array,
				default:[]
			}
		},
		data() {
			return {
				
			}
		},
		onLoad() {
		},
		methods: {
			// 点击选项卡修改选中页面
			activeTab: function(index) {
				// 把改变的index值传递回给父组件
				this.$emit("changeIndex",index);
			}
		}
	}
</script>

<style lang="scss" scoped>
	.uni-swiper-tab {
		border-bottom: none;
	}
	.swiper-tab-list {
		color: #969696;
		font-weight: bold;
		font-size: 28upx;
	}
	.active {
		position: relative;
		color: #343434 !important;
		&::after{
			content: '';
			position: absolute;
			bottom: 24upx;
			left: 50%;
			transform: translateX(-50%);
			height: 10upx;
			border-radius: 8upx;
			width: 40%;
			background-color: #fede33;
		}
	}
	
</style>
