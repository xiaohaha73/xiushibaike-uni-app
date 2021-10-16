<!--发布动态页面-->
<template>
	<view>
		<uni-nav-bar :statusBar="true" left-icon="arrowleft" rightText="发布" @clickLeft="back" @clickRight="submit">
			<view class="middle-title" @tap="selectHandle">
				{{selectedAuth}}
				<view class="iconfont icon-xialazhankai">
				</view>
			</view>
		</uni-nav-bar>

		<view class="uni-textarea">
			<textarea v-model="text" placeholder="说一句话吧~" />
		</view>

		<!--上传多图-->
		<view class="uni-list">
			<view class="uni-list-cell cell-pd">
				<view class="uni-uploader">
					<view class="uni-uploader-head">
						<view class="uni-uploader-title">点击可预览选好的图片</view>
						<view class="uni-uploader-info">{{imageList.length}}/9</view>
					</view>
					<view class="uni-uploader-body">
						<view class="uni-uploader__files">
							<block v-for="(image,index) in imageList" :key="index">
								<view class="uni-uploader__file" style="position: relative;">
									<view class="iconfont icon-shanchu" @tap="deleteImgHandle(index)"></view>
									<image class="uni-uploader__img" :src="image" :data-src="image" @tap="previewImage">
									</image>
								</view>
							</block>
							<view class="uni-uploader__input-box">
								<view class="uni-uploader__input" @tap="chooseImage"></view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>

		<!--弹出公告弹窗-->
		<view>
			<!-- 普通弹窗 -->
			<uni-popup ref="popup" background-color="#fff" :maskClick="false">
				<view class="popup-content">
					<image src="../../static/common/addinput.png" mode="widthFix"></image>
					<view style="margin-top: 20upx;">1、涉及黄色,政治,广告及骚扰信息</view>
					<view>2、涉及人身攻击</view>
					<view>3、留联系方式,透露他人隐私</view>
					<view>一经核实将被封禁,情节严重者永久封禁</view>
					<button type="primary" @tap="confirmHandle">朕知道了</button>
				</view>
			</uni-popup>
		</view>
	</view>
</template>

<script>
	import uniNavBar from "../../component/common/navbar/uni-nav-bar.vue"
	import permision from "@/common/permission.js"
	import uniPopup from "../../component/common/uni-popup/uni-popup.vue"
	var sourceType = [
		['camera'],
		['album'],
		['camera', 'album']
	]
	var sizeType = [
		['compressed'],
		['original'],
		['compressed', 'original']
	]
	export default {
		components: {
			uniNavBar,
			uniPopup
		},
		data() {
			return {
				// 选中的权限值
				selectedAuth: '所有人可见', //默认所有人可见
				imageList: [], // 要提交的图片列表
				text: '', // 要上传的文本内容
				sourceTypeIndex: 2,
				sourceType: ['拍照', '相册', '拍照或相册'],
				sizeTypeIndex: 2,
				sizeType: ['压缩', '原图', '压缩或原图'],
				countIndex: 8,
				count: [1, 2, 3, 4, 5, 6, 7, 8, 9]
			}
		},
		onLoad() {
			// this.imageList = [],
				this.sourceTypeIndex = 2,
				this.sourceType = ['拍照', '相册', '拍照或相册'],
				this.sizeTypeIndex = 2,
				this.sizeType = ['压缩', '原图', '压缩或原图'],
				this.countIndex = 8;
				
				// 调用从缓存中获取草稿内容的函数
				this.getDraftStorage();
				
		},
		methods: {
			// 返回前一页的点击事件
			back: function() {
				// 表单内容为空直接返回
				if (this.text.trim() === '' && this.imageList.length === 0) {
					uni.navigateBack({
						delta: 1
					})
				} else {
					uni.showModal({
						// title: '',
						content: '是否保存为草稿?',
						showCancel: true,
						cancelText: '不保存',
						confirmText: '保存',
						confirmColor: '#ffe934',
						cancelColor: '#cccccc',
						success: res => {
							// console.log(res);
							if (res.confirm) {
								// 需要保存
								const storageData = {
									text:this.text,
									imageList:this.imageList
								};
								uni.setStorageSync('draftStorage',JSON.stringify(storageData));
							}else {
								// 不保存的情况清理一下草稿缓存
								uni.removeStorageSync('draftStorage');
							}
							
							// 最后保不保存都要退出这个页面
							uni.navigateBack({
								delta: 1
							})

						}
					});
				}

			},
			// 从缓存中读取要发表的草稿
			getDraftStorage: function() {
				const storageData = uni.getStorageSync('draftStorage');
				if (storageData) {
					const dataObj = JSON.parse(storageData);
					this.imageList = dataObj.imageList;
					this.text = dataObj.text;
				}else {
					this.imageList = [];
					this.text = '';
				}
				// if (text !== as)
			},
			
			// 下拉弹窗点击事件
			selectHandle: function() {
				// 发布的动态哪些人能看
				const auth = ['所有人可见', '仅自己可见']
				uni.showActionSheet({
					itemList: auth,
					success: (res) => {
						// console.log(res);
						this.selectedAuth = auth[res.tapIndex]
					}
				})
			},
			// 提交动态的点击事件
			submit: function() {
				// console.log("提交！！");
				this.$refs.popup.open("center");
			},

			// 确认已读申明提交表单
			confirmHandle: function(e) {
				this.$refs.popup.close();
			},

			// 删除预览图片事件
			deleteImgHandle: function(index) {
				//console.log(index);
				this.imageList.splice(index, 1);
			},

			chooseImage: async function() {
				// #ifdef APP-PLUS
				// TODO 选择相机或相册时 需要弹出actionsheet，目前无法获得是相机还是相册，在失败回调中处理
				if (this.sourceTypeIndex !== 2) {
					let status = await this.checkPermission();
					if (status !== 1) {
						return;
					}
				}
				// #endif

				if (this.imageList.length === 9) {
					// 大于9张直接终止
					return false
				}
				uni.chooseImage({
					sourceType: sourceType[this.sourceTypeIndex],
					sizeType: sizeType[this.sizeTypeIndex],
					count: this.imageList.length + this.count[this.countIndex] > 9 ? 9 - this.imageList
						.length : this.count[this.countIndex],
					success: (res) => {
						this.imageList = this.imageList.concat(res.tempFilePaths);
					},
					fail: (err) => {
						console.log("err: ", err);
						// #ifdef APP-PLUS
						if (err['code'] && err.code !== 0 && this.sourceTypeIndex === 2) {
							this.checkPermission(err.code);
						}
						// #endif
						// #ifdef MP
						if (err.errMsg.indexOf('cancel') !== '-1') {
							return;
						}
						uni.getSetting({
							success: (res) => {
								let authStatus = false;
								switch (this.sourceTypeIndex) {
									case 0:
										authStatus = res.authSetting['scope.camera'];
										break;
									case 1:
										authStatus = res.authSetting['scope.album'];
										break;
									case 2:
										authStatus = res.authSetting['scope.album'] && res
											.authSetting['scope.camera'];
										break;
									default:
										break;
								}
								if (!authStatus) {
									uni.showModal({
										title: '授权失败',
										content: 'Hello uni-app需要从您的相机或相册获取图片，请在设置界面打开相关权限',
										success: (res) => {
											if (res.confirm) {
												uni.openSetting()
											}
										}
									})
								}
							}
						})
						// #endif
					}
				})
			},
			previewImage: function(e) {
				var current = e.target.dataset.src
				uni.previewImage({
					current: current,
					urls: this.imageList
				})
			},
			async checkPermission(code) {
				let type = code ? code - 1 : this.sourceTypeIndex;
				let status = permision.isIOS ? await permision.requestIOS(sourceType[type][0]) :
					await permision.requestAndroid(type === 0 ? 'android.permission.CAMERA' :
						'android.permission.READ_EXTERNAL_STORAGE');

				if (status === null || status === 1) {
					status = 1;
				} else {
					uni.showModal({
						content: "没有开启权限",
						confirmText: "设置",
						success: function(res) {
							if (res.confirm) {
								permision.gotoAppSetting();
							}
						}
					})
				}

				return status;
			}

		}
	}
</script>

<style lang="scss" scoped>
	.middle-title {
		display: flex;
		flex-direction: row;
		justify-content: center;
		margin: 0 auto;

		.iconfont {
			padding-right: 15upx;
		}
	}

	.uni-textarea uni-textarea {
		padding: 24upx 2%;
	}


	.uni-list {
		margin-top: 100upx;

		&::before {
			display: none;
		}

		&::after {
			display: none;
		}

		.uni-list-cell {
			padding: 0 20upx 0 20upx;

			.uni-uploader__input-box {
				background-color: #f5f5f5 !important;
				border: none;
			}
		}
	}

	.icon-shanchu {
		position: absolute;
		z-index: 4;
		background-color: #333333;
		padding: 4upx;
		color: white;
		border-radius: 8upx;
		top: 0;
		right: 0;
	}

	.popup-content {
		display: flex;
		flex-direction: column;
		padding: 20upx;

		image {
			width: 60%;
			margin: 0 auto;
		}

		view {
			margin-top: 10upx;
		}

		button {
			margin-top: 25upx;
			width: 95%;
			color: black;
			background-color: #ffe934;
		}
	}
</style>
