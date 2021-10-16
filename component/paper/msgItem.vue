<template>
	<uni-swipe-action-item :right-options="options" @click="swipeClick($event)">
		<view class="content-box" @tap="jumpHandle">
			<view class="avatar">
				<image src="../../static/demo/userpic/12.jpg"></image>
			</view>
			<view class="content">
				<view class="name">
					JIA一勺
				</view>
				<view class="msg">
					项目 '嗅事百科' 编译成功。前端运行日志，请另行在浏览器的控制台查看。
				</view>
			</view>
			<view class="box-right">
				<view class="time">
					13:58
				</view>
				<view class="count">
					1
				</view>
			</view>
		</view>
	</uni-swipe-action-item>
</template>

<script>
	import uniSwipeActionItem from "../common/uni-swipe/uni-swipe-action-item/uni-swipe-action-item.vue"
	export default {
		components: {
			uniSwipeActionItem
		},
		data() {
			return {
				// 左滑选项	
				options: [{
						text: '置顶'
					},
					{
						text: '标记为已读',
						style: {
							backgroundColor: 'rgb(254,156,1)'
						}
					},
					{
						text: '删除',
						style: {
							backgroundColor: 'rgb(255,58,49)'
						}
					}
				]
			}
		},
		methods: {
			swipeClick(e, index) {
				console.log(e);
			},
			
			// 聊天页面跳转函数
			jumpHandle: function() {
				uni.navigateTo({
					url:"../../pages/chat/chat?name=hahaha"
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.content-box {
		flex: 1;
		/* #ifdef APP-NVUE */
		justify-content: center;
		/* #endif */
		height: 140upx;
		// line-height: 120upx;
		box-sizing: border-box;
		// padding: 0 20upx 0 20upx;
		position: relative;
		background-color: #fff;
		border-bottom-color: #f5f5f5;
		border-bottom-width: 1px;
		border-bottom-style: solid;
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;

		.avatar {
			width: 100upx;
			height: 100upx;

			image {
				width: 100%;
				height: 100%;
				border-radius: 50%;
			}
		}

		.content {
			flex: 1;
			display: flex;
			flex-direction: column;
			height: 120upx;
			max-width: 60%;

			.name {
				flex: 1;
				line-height: 68upx;
			}

			.msg {
				flex: 1;
				color: #a8a8a8;
				font-size: 26upx;
				white-space: nowrap;
				overflow: hidden;
				text-overflow: ellipsis;
			}
		}

		.box-right {
			width: 120upx;
			height: 100%;
			// text-align: center;
			position: relative;
			.time {
				position: absolute;
				top: 20upx;
				left: 50%;
				transform: translateX(-50%);
				color: #d2d2d2;
				font-size: 26upx;
				line-height: 46upx;
			}

			.count {
				position: absolute;
				bottom: 20upx;
				left: 50%;
				transform: translateX(-50%);
				background-color: #ff6434;
				color: white;
				display: inline-block;
				padding: 0 10upx 0 10upx;
				border-radius: 20upx;
			}
		}
	}
</style>
