<template>
	<view class="content">
		<!-- <image class="logo" src="/static/logo.png"></image> -->
		<view class="text-area">
			<text class="title">{{title1}}</text>
			<navigator url="../detail/index?id=33" hover-class="navigator-hover">
				<button type="default">跳转到详情页</button>
			</navigator>
			<navigator url="../tab" hover-class="navigator-hover">
				<button type="default">跳转到tab</button>
			</navigator>
			
		</view>
		<view>
			<button type="primary" @click="ClickMe">我被点击了{{count}}次</button>
		</view>
		 <view class="image-content">
			<image mode="aspectFit" style="width: 200px; height: 200px; background-color: #eeeeee;" :src="src"
			></image>
		</view>
		<view class="common">
			全局样式
		</view>
		<view class="box">测试的文字</view>
		<view class="icon-edit edit"></view>字体图标
		<button type="primary" @click="upload">上传图标</button>
		<image :src="uploadImg" mode="aspectFit"></image>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title1: '我的主页',
				count: 0,
				uploadImg: '',
				src: 'https://img1.baidu.com/it/u=2969560901,1124562671&fm=26&fmt=auto'
			}
		},
		onLoad() {
			uni.getStorage({
				key: 'type',
				success: (res) => {
					console.log(res)
				}
			})
		},
		onPullDownRefresh() {
			console.log('refresh');
			setTimeout(function () {
				uni.stopPullDownRefresh();
			}, 1000);
		},
		methods: {
			ClickMe () {
				this.count++
			},
			upload () {
				uni.chooseImage({
					sizeType:['original', 'compressed'],
					success: (res) => {
						const src = res.tempFilePaths[0]
						this.uploadImg = src
						console.log(src, res)
						uni.previewImage({
							urls: res.tempFilePaths,
							longPressActions: {
								itemList: ['发送给朋友', '保存图片', '收藏'],
								success: function(data) {
									console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data.index + 1) + '张图片');
								},
								fail: function(err) {
									console.log(err.errMsg);
								}
							}
						})
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	@import url("./my.css");
	@import url("/static/iconfont/style.css");
	.content {
		/* display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center; */
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
	.box {
		width: 375rpx;
		height: 375rpx;
		background-color: #007AFF;
	}
	.concat {
		width: 50rpx;
		height: 50rpx;
	}
	.edit {
		color: #F63623;
		font-size: 28rpx;
		&::before {
			color: #F63623;
		}
	}
</style>
