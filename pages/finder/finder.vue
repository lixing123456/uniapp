<template>
	<view>
		<text @click="aaa">分享</text> 
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			aaa(){
				uni.navigateTo({
					url:"/pages/404/404?name=404"
				})
			}
		}
	}
</script>

<style>

</style>
