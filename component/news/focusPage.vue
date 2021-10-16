<template>
	<scroll-view scroll-y="true" style="height: 100%;" @scrolltolower="loadMore">
		<ListItem/>
		<ListItem/>
		<ListItem/>
		<ListItem/>
		<ListItem/>
		<ListItem/>
		<ListItem/>
	</scroll-view>
</template>

<script>
	import ListItem from "../common/listItem.vue"
	
	export default {
		components:{
			ListItem
		},
		data() {
			return {}
		},
		methods: {
			loadMore: function() {
				console.log("加载更多");
			}
		}
	}
</script>

<style>
</style>
