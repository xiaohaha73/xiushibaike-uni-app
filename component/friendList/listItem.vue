<template>
	<view class="item">
		<view class="item-left">
			<image src="../../static/demo/userpic/17.jpg" mode="widthFix" lazy-load></image>
			<view class="user">
				<view class="user-name">
					Supzeol
				</view>
				<view class="iconfont icon-nan">
					26
				</view>
				<!-- <view class="iconfont icon-nv">
					26
				</view> -->
			</view>
		</view>
		
		<view class="item-right">
			<view v-if="friendType === 0" class="iconfont icon-xuanze"></view>
			<view v-if="friendType === 2" class="iconfont icon-zengjia1"></view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			friendType: {
				type: Number,
				default:0 // 0 互关 1 关注 2 粉丝
			}
		},
		data() {
			return {}
		},
		methods:{}
	}
</script>

<style lang="scss" scoped>
	.item {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		width: 100%;
		border-bottom: 1px solid #cccccc;
		box-sizing: border-box;
		padding: 20upx;
		.item-left {
			display: flex;
			flex-direction: row;
			align-items: center;
			image {
				height: 80upx;
				width: 80upx;
				border-radius: 50%;
			}
			
			.user {
				margin-left: 20upx;
				
				.iconfont {
					font-size: 26upx;
					color: white;
					display: inline-block;
					padding: 0 8upx 0 8upx;
					border-radius: 14upx;
				}
				
				.icon-nan {
					background-color: #43b3ff;
				}
				
				.icon-nv {
					background-color: #ff698d;
				}
			}
		}
		
		.item-right {
			// #f87d22
			.icon-zengjia1 {
				color: #f87d22;
			}
		}
	}
</style>
