<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	@import './common/uni.css';
	/* iconfont图标css */
	@import './common/icon.css';
	/* 动画css */
	@import './common/animate.css';
	page {
		height: 100%;
	}
	
	.swiperBanner .uni-swiper-wrapper  {
		border-radius: 14upx;
		overflow: hidden !important;
	}
	
</style>
