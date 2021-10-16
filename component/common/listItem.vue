<template>
	<view class="list-item animated fadeInLeft fast">
		<view class="header">
			<view class="author">
				<image src="../../static/demo/userpic/10.jpg" mode="widthFix" lazy-load></image>
				<view class="author-name">
					三鱼先生
				</view>
				<view class="age woman">
					<!-- <view class="iconfont icon-nan"></view> -->
					<view class="iconfont icon-nv"></view>
					25
				</view>
			</view>
			<view class="btn-group">
				<view class="focus-btn">
					<view class="iconfont icon-zengjia"></view>
					关注
				</view>
				<view class="iconfont icon-guanbi"></view>
			</view>
		</view>
		<view class="media">

			<!--图片形式-->
			<!-- <view class="img-type">
				<view class="descrption">
					浅析插画设计中的风格和例子
				</view>
				<view class="img">
					<image src="../../static/demo/datapic/14.jpg" mode="widthFix"></image>
				</view>
			</view> -->

			<!--视频形式-->
			<!-- <view class="video-type">
				<view class="descrption">
					浅析插画设计中的风格和例子
				</view>
				<view class="video">
					<image src="../../static/demo/datapic/14.jpg" mode="widthFix"></image>
					<view class="play-btn iconfont icon-bofang"/>
					<view class="info">20w 次播放 2:47</view>
				</view>
			</view> -->

			<!--分享模式-->
			<view class="share">
				<image src="../../static/demo/datapic/15.jpg" mode="widthFix" lazy-load></image>
				<view class="text">
					浅析插画设计中的风格和例子
				</view>
			</view>
		</view>
		<view class="bottom">
			<view class="location">
				云南-玉溪
			</view>
			<view class="btn-group">
				<view class="btn">
					<view class="iconfont icon-zhuanfa"></view>
					36
				</view>
				<view class="btn">
					<view class="iconfont icon-xiaoxi"></view>
					37
				</view>
				<view class="btn">
					<view class="iconfont icon-dianzan"></view>
					37
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {}
		},
		methods: {}
	}
</script>
<style lang="scss" scoped>
	.list-item {
		padding: 20upx;
		display: flex;
		flex-direction: column;

		.header {
			display: flex;
			flex-direction: row;
			justify-content: space-between;

			.author {
				display: flex;
				flex-direction: row;
				align-items: center;

				image {
					height: 90upx;
					width: 90upx;
					border-radius: 50%;
				}

				.author-name {
					margin-left: 20upx;
					color: #414141;
				}

				.age {
					display: flex;
					flex-direction: row;
					align-items: center;
					color: white;
					font-size: 27upx;
					padding: 0 16upx;
					background-color: #44b3ff;
					margin-left: 20upx;
					border-radius: 20upx;
				}

				.woman {
					background-color: #eb3941;
					;
				}
			}

			.btn-group {
				display: flex;
				flex-direction: row;
				align-items: center;

				.focus-btn {
					display: flex;
					flex-direction: row;
					margin-right: 20upx;
					background-color: #f4f4f4;
					font-size: 30upx;
					padding: 10upx;
				}
			}
		}


		.media {
			.descrption {
				// margin-top: 20upx;
				text-align: left;
				padding-left: 10upx;
			}

			width: 100%;
			text-align: center;
			margin-top: 20upx;

			.img {
				width: 100%;
				height: 100%;
				margin-top: 20upx;

				image {
					// width: 776upx;
					// height: 364upx;
					width: 100%;
					border-radius: 20upx;
				}

			}

			.video {
				position: relative;
				margin-top: 20upx;

				image {
					width: 100%;
					border-radius: 20upx;
				}

				.play-btn {
					position: absolute;
					top: 50%;
					left: 50%;
					color: #ffffff;
					font-size: 120upx;
					transform: translate(-50%, -50%);

					&:active {
						color: #fede33 !important;
					}
				}

				.info {
					position: absolute;
					right: 16upx;
					background: rgba(51, 51, 51, 0.72);
					padding: 0 18upx 0 18upx;
					border-radius: 20upx;
					font-size: 28upx;
					bottom: 20upx;
					color: #ffffff;
				}
			}

			.share {
				display: flex;
				flex-direction: row;
				background-color: #f4f4f4;
				border-radius: 16upx;
				overflow: hidden;
				align-items: center;

				image {
					height: 30%;
					width: 30%;
					border-radius: 16upx;
				}

				.text {
					margin-left: 40upx;
					white-space: nowrap;
					overflow: hidden;
					text-overflow: ellipsis;
				}
			}

		}

		.bottom {
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			margin-top: 20upx;
			border-bottom: 2upx solid #cccccc;
			padding-bottom: 20upx;
			color: #3e3e3e;

			.location {}

			.btn-group {
				display: flex;
				flex-direction: row;

				.btn {
					display: flex;
					flex-direction: row;
					margin-left: 20upx;

					.iconfont {
						&:active {
							color: #fede33;
						}
					}
				}
			}
		}
	}
</style>
