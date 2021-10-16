<template>
	<!-- 热门分类组件 -->
	<view class="hotcate">
		<view class="header">
			<view class="header-left">
				热门分类
			</view>
			<view class="header-right" @tap="jumpPage">
				更多 >
			</view>
		</view>
		<view class="cate-list">
			<view class="cate-item" v-for="(item,index) in tags" :key="index">
				<text>{{item.name}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			tags: {
				type: Array,
				default:[]
			}
		},
		data() {
			return {}
		},
		methods:{
			// 跳转更多分类页面
			jumpPage: function() {
				uni.navigateTo({
					url:'../../pages/topicCate/topicCate'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.hotcate {
		padding: 20upx 20upx 50upx 20upx;
		border-bottom: 4upx solid #f4f4f4;
		.header {
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			font-size: 24upx;
			margin-bottom: 20upx;
			.header-right {
				color: #969696;
			}
		}
		
		.cate-list {
			margin-top: 30upx;
			display: flex;
			flex-direction: row;
			.cate-item {
				flex: 1;
				text-align: center;
				box-sizing: border-box;
				text {
					background-color: #f7f7f7;
					font-size: 24upx;
					color: #969696;
					padding: 10upx 20upx 10upx 20upx;
					border-radius: 10upx;
				}
			}
		}
	}
</style>
