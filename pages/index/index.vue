<template>
	<view class="container">

		<view class="intro" @click="aaa">本项目已包含uni ui组件，无需import和注册，可直接使用。。</view>
		<text class="intro">详见：</text>
		<uni-link :href="href" :text="href"></uni-link>
		<navigator url="/pages/404/404">404</navigator>
		<view>
			<navigator url="/subpages/chat/chat">前往在线聊天</navigator>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				href: 'https://uniapp.dcloud.io/component/README?id=uniui'
			}
		},
		onLoad:function(option) {
			console.log('onLoad',option)
			console.log(getCurrentPages(),'111')
		},
		onReady() {
			console.log('onReady')
		},
		onShow() {
			console.log('onShow')
		},
		onPullDownRefresh() {
			console.log('刷新了')
			setTimeout(()=>{uni.stopPullDownRefresh()},2000)
			
		},
		onShareAppMessage() {
			console.log('分享')
		},
		methods: {
			aaa() {
				let aaa='404'
				uni.navigateTo({
					url:"/pages/404/404?name=404"
				})
			}
		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
</style>
