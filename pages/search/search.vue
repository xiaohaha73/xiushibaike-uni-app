<template>
	<view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		mounted() {
			// 关闭返回的箭头按钮
			// var a = document.getElementsByClassName('uni-page-head-hd')[0]
			// a.style.display = 'none';
		},
		// 头部标题按钮监听事件
		onNavigationBarButtonTap(e) {
			// console.log(e);
			if (e.index === 0) {
				// 取消按钮
				uni.navigateBack({
					delta:1
				});
			}
		},
		// 搜索框内容改变事件
		onNavigationBarSearchInputChanged(e) {
			console.log(e);
		},
		// 软键盘点击搜索按钮事件
		onNavigationBarSearchInputConfirmed(e) {
			console.log(e);
		}
		
	}
</script>

<style lang="scss" scoped>

</style>
