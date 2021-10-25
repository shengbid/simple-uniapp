<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<view>
			<view class="item" v-for="item in list" :key="item.id">
				<view class="name">
					名称: {{item.name}}
				</view>
				<view class="name">
					价格: {{item.price}}
				</view>
			</view>
		</view>
		<view class="child">
			<userInfo @changeName="changeName" :userInfo="user" />
		</view>
		<view class="name">
			改变的名字{{name}}
		</view>
		<view>
			全局信息{{login.account}}
		</view>
	</view>
</template>

<script>
	import userInfo from '@/components/userInfo.vue'
	export default {
		components: {
			userInfo
		},
		data() {
			return {
				title: 'Hello6',
				name: '',
				user: {
					name: '张三',
					age: 44
				},
				login: {},
				list: [
					{
						id: 1,
						name: '商品1',
						price: 9999
					},
					{
						id: 2,
						name: '商品2',
						price: 555
					},
					{
						id: 3,
						name: '商品3',
						price: 800
					}
				]
			}
		},
		onLoad() {
			this.login = getApp().globalData.loginInfo
			uni.setStorage({
				key: 'type',
				data: 'warning'
			})
		},
		methods: {
			changeName(name) {
				this.name = name
			}
		},
		onPullDownRefresh() {
			console.log('refresh');
			setTimeout(() => {
				this.list.push({
					id: 5,
					name: '刷新的名称',
					price: 888
				})
				uni.stopPullDownRefresh();
			}, 1000);
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
