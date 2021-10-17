<template>
	<view class="content">
		<!-- <image class="logo" src="/static/logo.png"></image> -->
		<view class="text-area">
			<text class="title">{{title1}}</text>
			<navigator url="../detail/index?id=33" hover-class="navigator-hover">
				<button type="default">跳转到详情页</button>
			</navigator>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title1: '我的主页'
			}
		},
		onLoad() {

		},
		onPullDownRefresh() {
			console.log('refresh');
			setTimeout(function () {
				uni.stopPullDownRefresh();
			}, 1000);
		},
		methods: {

		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
