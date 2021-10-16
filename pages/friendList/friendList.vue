<template>
	<view>
		<!-- tab栏 -->
		<view class="tab">
			<view class="tab-item" :class="currentIndex===0? 'active':''" @tap="activeHandle(0)">
				互关 10
			</view>
			<view class="tab-item" :class="currentIndex===1? 'active':''" @tap="activeHandle(1)">
				关注 20
			</view>
			<view class="tab-item" :class="currentIndex===2? 'active':''" @tap="activeHandle(2)">
				粉丝 1000
			</view>
		</view>
		<!-- 主显示区 -->
		<view class="main">
			<swiper :current="currentIndex" @change="indexChange" :style="{height: swiperHeight + 'px'}">
				<swiper-item v-if="true" key="0">
					<scroll-view scroll-y="true" style="height: 100%;">
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
						<ListItem :friendType="0"/>
					</scroll-view>
				</swiper-item>
				<swiper-item v-if="true" key="1">
					<scroll-view scroll-y="true" style="height: 100%;">
						<ListItem :friendType="1"/>
					</scroll-view>
				</swiper-item>

				<swiper-item v-if="true" key="2">
					<scroll-view scroll-y="true" style="height: 100%;">
						<ListItem :friendType="2"/>
					</scroll-view>
				</swiper-item>

				<!--列表为空时显示的样式-->
				<swiper-item v-else>
					<Nothing />
				</swiper-item>

			</swiper>
		</view>
	</view>
</template>

<script>
	import Nothing from "../../component/common/nothing.vue"
	import ListItem from "../../component/friendList/listItem.vue"
	export default {
		components: {
			Nothing,
			ListItem
		},
		data() {
			return {
				currentIndex: 0, // 默认选中的tab卡
				swiperHeight: 0 // 滑动页面的高度
			}
		},
		onNavigationBarButtonTap(e) {
			// console.log(e);
			if (e.index === 0) {
				console.log("点击了取消按钮");
			}
		},
		onLoad() {
			// 需要动态获取屏幕的高度然后赋值给swiper不然不会生效
			uni.getSystemInfo({
				success: (res) => {
					// console.log(res.windowHeight);
					this.swiperHeight = res.windowHeight - 44;
				}
			});
		},
		methods: {
			// tab选中切换函数
			activeHandle: function(index) {
				this.currentIndex = index;
			},

			// 滑动切换页面函数
			indexChange: function(e) {
				// console.log(e);
				this.currentIndex = e.detail.current;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.tab {
		display: flex;
		flex-direction: row;
		height: 80upx;
		align-items: center;

		.tab-item {
			flex: 1;
			text-align: center;
			color: #8e8e8e;
			font-size: 26upx;
			font-weight: bold;
		}

		.active {
			color: #303030;
			position: relative;

			&::after {
				content: '';
				height: 8upx;
				width: 70upx;
				background-color: #fede33;
				position: absolute;
				bottom: -10upx;
				left: 50%;
				border-radius: 8upx;
				transform: translateX(-50%);
			}
		}
	}

	.main {
		box-sizing: border-box;
		padding: 0 20upx 0 20upx;
		// margin-top: 80upx;
		overflow: hidden;
	}
</style>
