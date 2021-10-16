<template>
	<view>
		<!-- 聊天记录时间显示 -->
		<view class="chat-time" v-if="time">
			{{time}}
		</view>
		<!-- 发送出去类型的气泡 -->
		<view class="chat-item sendMsg" v-if="chatType === 0">
			<view class="msg-box">
				{{msg}}
			</view>
			<image :src="avatar" mode="widthFix"></image>
		</view>
		
		<!-- 接收到的类型的气泡 -->
		<view class="chat-item accMsg" v-if="chatType === 1">
			<image :src="avatar" mode="widthFix"></image>
			<view class="msg-box">
				{{msg}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			chatType: {
				type: Number, // 聊天框类型0 发送出去 1接收到的
				default:1
			},
			msg: {
				type: String,
				default:''
			},
			time: {
				type: String,
				default:''
			},
			avatar: {
				type: String,
				default:''
			}
		}
	}
</script>

<style lang="scss" scoped>
	.chat-item {
		width: 100%;
		display: flex;
		flex-direction: row;
		// justify-content: flex-end;
		padding: 20upx;
		box-sizing: border-box;
		image {
			height: 100upx;
			width: 100upx;
			border-radius: 50%;
		}
		
		.msg-box {
			max-width: 60%;
			box-sizing: border-box;
			padding: 20upx;
			border-radius: 15upx;
			margin-top: 10upx;
			margin-bottom: 10upx;
			background-color: #f4f4f4;
			position: relative;
		}
		
	}
	
	.sendMsg {
		justify-content: flex-end !important;
		.msg-box {
			margin-right: 20upx;
			
			&::after {
				content: '';
				position: absolute;
				width: 0;
				height: 0;
				border-top: 30upx solid #f4f4f4;
				border-right: 30upx solid transparent;
				right: -24upx;
				top: 20upx;
			}
		}
	}
	
	.accMsg {
		justify-content: flex-start !important;
		.msg-box {
			margin-left: 20upx;
			
			&::after {
				content: '';
				position: absolute;
				width: 0;
				height: 0;
				top: 20upx;
				left: -24upx;
				border-top: 30upx solid #f4f4f4;
				border-left: 30upx solid transparent;
			}
		}
	}
	
	.chat-time {
		// height: 40upx;
		// line-height: 40upx;
		text-align: center;
		color: #959595;
		font-size: 26upx;
	}
	
</style>
