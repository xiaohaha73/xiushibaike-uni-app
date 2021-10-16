<template>
	<view class="list-item animated fadeInLeft fast">
		<view class="item-header">
			<view class="header-left">
				<view class="avatar">
					<image src="../../static/demo/userpic/10.jpg" mode="widthFix" lazy-load/>
					法外狂徒张三
				</view>
			</view>
			
			<view class="header-right">
				<view class="focus-btn" @tap="focusHandle">
					<view class="iconfont icon-zengjia"></view>
					关注
				</view>
				<view class="close-btn">
					<view class="iconfont icon-guanbi"></view>
				</view>
			</view>
			
		</view>
		<view class="item-center">
			<view class="item-title">你很勇哦</view>
			<!--图片模式-->
			<!-- <view class="show-media">
				<image src="../../static/demo/datapic/1.jpg" mode="widthFix" lazy-load></image>
			</view> -->
			<!--视频模式-->
			<view class="play-media">
				<image src="../../static/demo/datapic/1.jpg" mode="widthFix" lazy-load></image>
				<view class="play-btn iconfont icon-bofang"/>
				<view class="info">20w 次播放 2:47</view>
			</view>
			
		</view>
		<view class="item-bottom">
			
			<view class="bottom-group">
				<view class="btn-group">
					<view
					 class="agree-btn iconfont icon-icon_xiaolian-mian"
					  :class="status === 1?'active':''"
					  @tap="agreeHandle(1)"
					></view>
					{{agreeNum}}
				</view>
				<view class="btn-group">
					<view
					 class="disagree-btn iconfont icon-kulian"
					  :class="status === 2?'active':''"
					  @tap="agreeHandle(2)"
					  ></view>
					{{disagreeNum}}
				</view>
			</view>
			
			<view class="bottom-group">
				<view class="btn-group">
					<view class="commment-btn iconfont icon-xiaoxi"></view>
					21
				</view>
				<view class="btn-group">
					<view class="share-btn iconfont icon-zhuanfa"></view>
					14
				</view>
			</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 点赞或者点踩状态
				status:0, // 0 都没点 1 点赞 2 点踩
				agreeNum: 21, // 点赞数
				disagreeNum: 4  // 点踩数
			}
		},
		onLoad() {
	
		},
		methods: {
			// 关注好友点击事件
			focusHandle: function() {
				uni.showToast({
					icon:'success',
					title:'关注成功'
				})
			},
			
			// 动态点赞和点踩事件
			agreeHandle: function(status) {
				// console.log(this.status);
				if (this.status === status) { // 取消点在或者点踩
					this.status = 0; // 回归到未点击任何按钮的状态
					switch (status) {
						case 1:
							this.agreeNum -= 1;
							break;
						case 2:
							this.disagreeNum -= 1;
							break;
					}
					return false
				}
				if (this.status === 0) {
					// 还未点过踩或者点过赞
					this.status = status;
					switch (status) {
						case 0: 
							break;
						case 1:
							this.agreeNum += 1;
							break;
						case 2:
							this.disagreeNum += 1;
							break;
					}
				}else {
					// 已经点过踩或者赞了
					this.status = status;
					switch (status) {
						case 1:
							this.agreeNum += 1;
							this.disagreeNum -= 1;
							break;
						case 2:
							this.disagreeNum += 1;
							this.agreeNum -= 1;
							break;
					}
				}
				
			}
			
		}
	}
</script>

<style lang="scss" scoped>
	$themBackground: #ffe03d;
	
	.list-item {
		width: 100%;
		display: flex;
		flex-direction: column;
		padding: 15upx 27upx 40upx 27upx;
		text-align: center;
		box-sizing: border-box;
		border-bottom: 2upx solid #cccccc;
		.item-header {
			height: 100upx;
			display: flex;
			flex-direction: row;
			
			.header-left {
				flex: 1;
				display: flex;
				flex-direction: row;
				justify-content: flex-start;
				.avatar {
					display: flex;
					flex-direction: row;
					align-items: center;
					color: #9e9e9e;
					image {
						height: 90upx;
						width: 90upx;
						border-radius: 50%;
						margin-right: 27upx;
					}
	
				}
	
			}
	
			.header-right {
				flex: 1;
				display: flex;
				flex-direction: row;
				justify-content: flex-end;
				align-items: center;
				
				.focus-btn {
					border-radius: 8upx;
					display: flex;
					flex-direction: row;
					align-items: center;
					padding: 5upx 10upx 5upx 10upx;
					background-color: #f4f4f4;
					margin-right: 27upx;
				}
				
				.close-btn {
					color: #9e9e9e;
				}
			}
		}
		
		.item-center {
			margin-top: 7upx;
			width: 100%;
			
			.item-title {
				text-align: left;
				height: 100upx;
				line-height: 100upx;
				font-size: 36upx;
				font-weight: bold;
			}
			.show-media {
				image {
					// width: 776upx;
					// height: 364upx;
					width: 100%;
					border-radius: 11upx;
				}
			}
			
			// 视频播放
			.play-media {
				position: relative;
				image {
					// width: 776upx;
					// height: 364upx;
					width: 100%;
					border-radius: 11upx;
				}
				
				.play-btn {
					position: absolute;
					top: 50%;
					left: 50%;
					color: #ffffff;
					font-size: 120upx;
					transform: translate(-50%,-50%);
					&:active {
						color: $themBackground !important;
					} 
				}
				.info {
					position: absolute;
					right: 16upx;
					background: rgba(51,51,51,0.72);
					padding: 0 18upx 0 18upx;
					border-radius: 20upx;
					font-size: 28upx;
					bottom: 20upx;
					color: #ffffff;
				}
				
			}
			
		}
		
		.item-bottom {
			margin-top: 30upx;
			width: 100%;
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			
			.bottom-group {
				display: flex;
				flex-direction: row;
				.btn-group {
					display: flex;
					flex-direction: row;
					align-items: center;
					color: #9e9e9e;
					.iconfont {
						margin-right: 15upx;
						&:active {
							color: $themBackground !important;
						}
					}
					.active {
						color: $themBackground !important;
					}
					
					.disagree-btn {
						font-size: 36upx;
						
					}
					
					// 图标选中样式
					.actived-btn {
						color: $themBackground;
					}
					&:nth-child(2) {
						margin-left: 26upx;
					}
				}
				
				
			}
		}
		
	}
	
</style>
