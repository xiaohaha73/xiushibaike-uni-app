<template>
	<view>
		<!-- 聊天记录列表 -->
		<scroll-view id="scroll" scroll-y="true" :scroll-top="scrollTop" :style="{height:scrollHeight + 'px'}">
			<view class="chat-list" v-for="(item,index) in msgList" :key="index">
				<ChatMsg :chatType="item.chatType" :msg="item.msg" :time="item.formatTime" :avatar="item.avatar" />
			</view>
		</scroll-view>
		<!-- 聊天发送组件 -->
		<SendBox @sendMsg="sendHandle" />
	</view>
</template>

<script>
	// 时间格式化工具
	import timeUtils from "../../common/js/time.js"

	import SendBox from "../../component/chat/sendBox.vue"
	import ChatMsg from "../../component/chat/chatMsg.vue"
	export default {
		components: {
			SendBox,
			ChatMsg
		},
		data() {
			return {
				msgList: [], // 消息列表
				scrollTop: 0, // 聊天列表距离上方的高度
				scrollHeight: 0, // 滚动框的高度能显示的高度
				scrollItemsHeight: 0 // 滚动框中所有元素的总高度
			}
		},
		onLoad(option) {
			// console.log(option.name);
			uni.setNavigationBarTitle({
				title: option.name
			})

			// 初始化滚动列表的高度
			// uni.getSystemInfo({
			// 	success: (res) => {
			// 		// console.log(res.windowHeight);
			// 		this.scrollHeight = res.windowHeight - 44;
			// 	}
			// });


			// 获取聊天记录
			this.getData();

		},
		onReady() {
			const res = uni.getSystemInfoSync();
			this.scrollHeight = res.windowHeight - 44;
			// 初始化滚动栏滑到最底部只能在created中执行
			this.scrollToBottom();
		},
		methods: {
			getData: function() {
				// 模拟聊天记录
				var msgList = [{
						msg: "哈哈哈哈哈",
						chatType: 0, // 0 代表发送出去的
						avatar: "../../static/demo/demo6.jpg",
						time: 1632912200,
					},
					{
						msg: "你很勇哦",
						chatType: 1,
						avatar: "../../static/demo/demo6.jpg",
						time: 1632912201,
					}
				];


				// 格式化显示消息的时间
				if (msgList.length > 0) {
					for (var i = 0; i < msgList.length; i++) {
						var preTime = i > 0 ? msgList[i - 1].time : 0;
						// 添加一个格式化时间
						msgList[i].formatTime = timeUtils.gettime.getChatTime(msgList[i].time, preTime);
					}
				}

				this.msgList = msgList
			},

			// 滚动栏滚动到最底部函数
			scrollToBottom: function() {
				let query = uni.createSelectorQuery();
				query.selectAll('.chat-list').boundingClientRect();
				query.exec((res) => {
					// 遍历循环计算高度
					// console.log(res[0]);
					this.scrollItemsHeight = 0;
					res[0].forEach((item)=> {
						// console.log(item);
						this.scrollItemsHeight += item.height;
					})
					
					// 如果总高度大于了显示区域的高度就滑动到最底部
					if (this.scrollItemsHeight > this.scrollHeight) {
						this.scrollTop = this.scrollItemsHeight;
					}
					
				})

			},

			// 发送消息函数按钮触发的事件
			sendHandle: function(msg) {
				// console.log(msg);
				var now_time = new Date().getTime();
				var last_time = this.msgList[this.msgList.length - 1].time;
				// 构建消息框
				var msgObj = {
					msg: msg,
					chatType: 0, // 0 代表发送出去的
					avatar: "../../static/demo/demo6.jpg",
					time: now_time,
					formatTime: timeUtils.gettime.getChatTime(now_time, last_time)
				};

				this.msgList.push(msgObj);
				setTimeout(()=>{ // 用异步执行 发现会每次元素都少一个所以搞一个延时
					// 执行滑动到最底部的函数
					this.scrollToBottom();
				})
				
			}
		}
	}
</script>

<style lang="scss" scoped>
	.chat-list {
		width: 100%;
		display: flex;
		flex-direction: column;
	}
</style>
