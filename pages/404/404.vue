<template>
	<view>
	<h1>当前页面不存在</h1>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		onLoad(options) {
			console.log(options)
			setTimeout(()=>{
				uni.switchTab({
					url:'/pages/index/index?name=aaa'
				})
			},2000)
		},
		onHide() {
			console.log('onHide')
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
