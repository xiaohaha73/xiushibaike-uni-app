<template>
	<view class="news-item" @tap="jumpPage">
		<image src="../../static/demo/topicpic/12.jpeg"></image>
		<view class="news-right">
			<view class="title">
				#淘宝记录薄#
			</view>
			<view class="content">
				85斤到120斤 我的富婆人生
			</view>
			<view class="desc">
				动态 545 今日 720
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {}
		},
		methods:{
			// 跳转详情页面函数
			jumpPage:function() {
				uni.navigateTo({
					url:'../../pages/topicDetail/topicDetail'
				})
			}
		}
		
	}
</script>

<style lang="scss" scoped>
	.news-item {
		padding: 20upx 0 20upx 0;
		display: flex;
		flex-direction: row;
		border-bottom: 4upx solid #f4f4f4;
		image {
			height : 180upx;
			width: 180upx;
			border-radius: 10upx;
			margin-right: 24upx;
		}
		
		.news-right {
			line-height: 48upx;
			padding-top: 18upx;
			.content ,.desc{
				font-size: 26upx;
				color: #969696;
			}
		}
	}
</style>
