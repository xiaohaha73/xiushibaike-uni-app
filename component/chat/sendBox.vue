<template>
	<view class="input-box">
		<input type="text" placeholder="文明发言" v-model="sendText"/>
		<view class="iconfont icon-fabu send" @tap="sendHandle"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sendText: "" // 发送的文字内容
			}
		},
		methods: {
			// 发送消息函数
			sendHandle: function() {
				// console.log(this.sendText);
				if (this.sendText.trim().length === 0) {
					return false;
				}
				this.$emit("sendMsg",this.sendText)
				// 清空输入框内容
				this.sendText = "";
			}
		}
	}
</script>

<style lang="scss" scoped>
	.input-box {
		position: fixed;
		z-index: 9999;
		width: 100%;
		height: 100upx;
		bottom: 0;
		left: 0;
		border-top: 2upx solid #f4f4f4;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		box-sizing: border-box;
		padding: 20upx;
		background-color: white;
		input {
			flex: 1;
			background-color: #f7f7f7;
			height: 65upx;
			border-radius: 8upx;
			padding-left: 20upx;
			font-size: 28upx;
		}
		
		.send {
			width: 100upx;
			text-align: center;
			height: 100%;
			font-size: 40upx;
			margin-top: 20upx;
		}
		
	}
</style>
