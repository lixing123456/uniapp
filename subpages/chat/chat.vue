<template>
	<view class="container">

		<!-- 聊天列表 -->
		<view class="chat-body">
			<block v-for="(item,index) in chatList" :key="index">
				<view class="chat-one" v-if="!item.isMe">
					<image class="chat-face" src="/static/19042219.jpg" mode=""></image>
					<view class="chat-box">
						<view class="chat-sender">
							旅行者
						</view>
						<view class="chat-content" v-if="item.type==='txt'">
							{{item.content}}
						</view>
						<image v-if="item.type==='img'" class="chat-img" :src="item.content" mode="widthFix"></image>
					</view>
				</view>


				<view v-else class="chat-one chat-one-mine">
					<view class="chat-one chat-one-mine">
						<view class="chat-box">
							<text v-if="item.type==='txt'" class="chat-content">{{item.content}}</text>
							<image v-if="item.type==='img'" class="chat-img" :src="item.content" mode="widthFix">
							</image>
						</view>
						<image class="chat-face" src="/static/19042219.jpg"></image>
					</view>
				</view>
			</block>
		</view>
		<!-- 聊天输入 -->
		<view class="chat-footer">
			<input class="msg-input" type="text" cursor-spacing="16" value="" v-model="myInput" />
			<image class="img-chose" src="/static/logo.png" mode="" @click="choseImgAndSend"></image>
			<view class="send-btn" @click="sendMsg">
				发送
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 保存聊天的内容
				chatList: [{
					isMe: false,
					type: 'txt',
					content: '旅行者你好，你想和我说什么'
				}, {
					isMe: false,
					type: 'img',
					content: '/static/logo.png'
				}, {
					isMe: true,
					type: 'txt',
					content: '玩得开心'
				}, {
					isMe: true,
					type: 'img',
					content: '/static/logo.png'
				}],
				name: '1111',
				myInput: ''
			}
		},
		onShow() {
			if (uni.getStorageSync('chatList')) {
				this.chatList = JSON.parse(uni.getStorageSync('chatList'))

				setTimeout(() => {
					uni.pageScrollTo({
						scrollTop: 9999999,
						duration: 0
					})
				}, 100)
			}
		},
		methods: {

			choseImgAndSend() {
				const that = this
				uni.chooseImage({
					count: 6, //默认9
					sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album'], //从相册选择
					success: function(res) {
						console.log(JSON.stringify(res.tempFilePaths[0]));
						let senMsg = {
							isMe: true,
							type: 'img',
							content: res.tempFilePaths[0]
						}
						that.chatList.push(senMsg)

						let resMsg = {
							isMe: false,
							type: 'img',
							content: res.tempFilePaths[0]
						}
						that.chatList.push(resMsg)
						setTimeout(() => {
							uni.pageScrollTo({
								scrollTop: 9999999,
								duration: 0
							})
						}, 100)

						uni.setStorageSync('chatList', JSON.stringify(that.chatList))
					}
				});
			},
			sendMsg() {
				let that = this
				if (!that.myInput) return
				let senMsg = {
					isMe: true,
					type: 'txt',
					content: that.myInput
				}
				that.chatList.push(senMsg)

				let resMsg = {
					isMe: false,
					type: 'txt',
					content: that.myInput
				}
				that.chatList.push(resMsg)

				setTimeout(() => {
					uni.pageScrollTo({
						scrollTop: 9999999,
						duration: 0
					})
				}, 100)

				uni.setStorageSync('chatList', JSON.stringify(that.chatList))
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		background-color: #F1F1F1;
		min-height: 100vh;
	}

	.chat-body {
		padding-bottom: 178upx;

		.chat-time {
			text-align: center;
			color: #888;
			padding: 40upx 0 0;
		}

		.chat-one {
			display: flex;
			flex-direction: row;
			flex-wrap: wrap;
			justify-content: flex-start;
			align-items: flex-start;
			padding: 20upx 0;
		}

		.chat-one-begin {
			padding: 40upx 0 0;
		}

		.chat-one-mine {
			justify-content: flex-end;
		}

		// .chat-two-mine {
		// 	width: 99%;
		// }

		.chat-face {
			width: 84upx;
			height: 84upx;
			border-radius: 10upx;
			margin-left: 40upx;
		}

		.chat-one-mine .chat-face {
			margin-left: 0;
			margin-right: 40upx;
		}

		.chat-box {
			max-width: calc(100%-290upx);
			margin-left: 20upx;
			font-size: 30upx;
		}

		.chat-one-mine .chat-box {
			margin-right: 20upx;
		}

		.chat-sender {
			color: #888;
			font-size: 28upx;
			margin-top: -8upx;
			margin-bottom: 10upx;
		}

		.chat-content {
			background-color: #fff;
			border-radius: 5px;
			padding: 10px;
			// margin-right: 20upx;

			.micon {
				margin-right: 20upx;
				color: #666;
			}
		}

		.chat-img {
			float: left;
			max-width: 60%;
			border-radius: 5px;
		}

		.chat-one-mine .chat-img {
			float: right;
		}
	}

	.chat-footer {
		width: 670upx;
		padding: 0 40upx;
		height: 120upx;
		position: fixed;
		bottom: 0;
		left: 0;
		background-color: #F1F1F1;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-around;
		align-items: center;
		align-content: center;
		border-top: 1upx solid #ddd;

		.msg-input {
			background-color: #fff;
			width: calc(100%-300upx);
			height: 70upx;
			line-height: 70upx;
			font-size: 30upx;
			border-radius: 10upx;
			padding: 0 20upx;
		}

		.img-chose {
			height: 70upx;
			width: 70upx;
		}

		.send-btn {
			height: 60upx;
			line-height: 60upx;
			width: 120upx;
			text-align: center;
			background-color: green;
			color: #FFFFFF;
			border-radius: 12upx;
		}
	}
</style>
