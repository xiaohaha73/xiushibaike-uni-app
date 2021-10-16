<template>
	<view>
		<view class="mask" v-show="isShow" @tap="cancelShow"></view>
		<view class="pop-menu" v-show="isShow">
			<view class="iconfont icon-sousuo" hover-class="active" @tap="addFriend">
				加嗅友
			</view>
			<view class="iconfont icon-qingchu" hover-class="active" @tap="clear">
				清除缓存
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			isShow: {
				type: Boolean,
				default:false
			}
		},
		data() {
			return {
				
			}
		},
		methods:{
			// 取消显示函数
			cancelShow: function(){
				this.$emit("close");
			},
			// 添加好友事件
			addFriend: function(){
				// 关闭菜单
				this.$emit("close");
			},
			// 清除缓存事件
			clear: function() {
				// 关闭菜单
				this.$emit("close");
			}
		}
	}
</script>
<style lang="scss" scoped>
	.mask {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		z-index: 4999;
		// background: #cccccc;
	}
	.pop-menu {
		position: fixed;
		z-index: 5000;
		width: 300upx;
		// height: 80upx;
		background-color: white;
		right: 0;
		top: 6upx;
		box-shadow: -1upx 1upx 12upx #cccccc;
		border-radius: 8upx;
		color: #444444;
		font-weight: bold;
		.iconfont {
			height: 80upx;
			line-height: 80upx;
			box-sizing: border-box;
			padding-left: 20upx;
			font-size: 28upx;
		}
		
		.active {
			background: #e5e5e5;
		}
		
	}
</style>
