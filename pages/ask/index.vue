<template>
	<view class="container">
		<view class="banner">
			<u-image width="100%" height="300rpx" :src="src"></u-image>
		</view>
		<view class="make">
			<u-button type="primary">制作</u-button>
		</view>
		<view class="study">
			<u-button type="primary">学习</u-button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				src: 'https://cdn.uviewui.com/uview/example/fade.jpg',
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container{
		.make{
			width: 80%;
			margin: 100rpx auto;
		}
		
		.study{
			width: 80%;
			margin: 100rpx auto;
		}
	}
</style>
