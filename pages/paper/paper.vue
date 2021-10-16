<template>
	<view class="paper">
		<PopMenu :isShow="isShow" @close="closeMenu"/>
		<view class="msg-list">
			<uni-swipe-action ref="swipeAction">
				<MsgItem />
				<MsgItem />
				<MsgItem />
				<MsgItem />
				<MsgItem />
				<MsgItem />
			</uni-swipe-action>
		</view>
	</view>
</template>

<script>
	import MsgItem from "../../component/paper/msgItem.vue"
	import uniSwipeAction from "../../component/common/uni-swipe/uni-swipe-action/uni-swipe-action.vue"
	import PopMenu from "../../component/paper/popMenu.vue"
	export default {
		components: {
			MsgItem,
			uniSwipeAction,
			PopMenu
		},
		onPullDownRefresh() { // 监听下拉刷新事件
			setTimeout(() => {
				uni.stopPullDownRefresh();
			}, 3000)
		},
		onNavigationBarButtonTap(e) { // 顶部标题按钮点击事件
			// console.log(e);
			switch (e.index) {
				case 0:
					// console.log("点击了左侧按钮");
					// 如果右边的菜单还打开着也需要关闭
					this.closeMenu();
					uni.navigateTo({
						url:"../friendList/friendList"
					})
					break;
				case 1:
					// console.log("点击了右侧按钮");
					this.menuToggle();
					break;
			}
		},
		data() {
			return {
				// 控制顶部菜单栏的弹出
				isShow: false // 默认为不显示
			}
		},
		methods: {
			// 控制弹出或关闭菜单函数
			menuToggle: function() {
				this.isShow = !this.isShow
				// console.log(this.isShow);
			},
			// 关闭菜单
			closeMenu: function() {
				this.isShow = false;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.paper {
		position: relative;
	}

	.msg-list {
		box-sizing: border-box;
		padding: 20upx 20upx 120upx 20upx;
	}
</style>
