<template>
	<view class="box">
		<view>
			<u-tabs-swiper 
				ref="uTabs" 
				:list="list" 
				:current="current" 
				@change="tabsChange" 
				:is-scroll="false"
				swiperWidth="750"></u-tabs-swiper>
		</view>
		<u-dropdown>
			<u-dropdown-item v-model="value1" title="距离" :options="options1"></u-dropdown-item>
			<u-dropdown-item v-model="value2" title="温度" :options="options1"></u-dropdown-item>
		</u-dropdown>
		<swiper :current="swiperCurrent" @transition="transition" @animationfinish="animationfinish" style="height: 800px;">
			<swiper-item class="swiper-item" v-for="(sitem, index) in swiperTabs" :key="index">
				<scroll-view scroll-y style="width: 100%;" @scrolltolower="onreachBottom" @touchmove.stop.prevent="()=>{}">
					<u-card 
						:title="title" 
						:sub-title="subTitle" 
						:thumb="thumb" 
						v-for="(item,index) in tabs"
						:key="index">
						<view class="" slot="body">
							<view class="u-body-item u-flex u-border-bottom u-col-between u-p-t-0">
								<view class="u-body-item-title u-line-2">{{item.desc}}</view>
								<image
									src="https://img11.360buyimg.com/n7/jfs/t1/94448/29/2734/524808/5dd4cc16E990dfb6b/59c256f85a8c3757.jpg"
									mode="aspectFill"></image>
							</view>
							<view class="u-body-item u-flex u-row-between u-p-b-0">
								<view class="u-body-item-title u-line-2">釉色渲染仕女图韵味被私藏，而你嫣然的一笑如含苞待放</view>
								<image
									src="https://img12.360buyimg.com/n7/jfs/t1/102191/19/9072/330688/5e0af7cfE17698872/c91c00d713bf729a.jpg"
									mode="aspectFill"></image>
							</view>
						</view>
						<view class="" slot="foot">
							<u-icon name="chat-fill" size="34" color="" label="30评论"></u-icon>
						</view>
					</u-card>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [{
					name: '十年'
				}, {
					name: '青春'
				}, {
					name: '之约'
				}],
				// 因为内部的滑动机制限制，请将tabs组件和swiper组件的current用不同变量赋值
				current: 0, // tabs组件的current值，表示当前活动的tab选项
				swiperCurrent: 0, // swiper组件的current值，表示当前那个swiper-item是活动的
				tabs: [],
				swiperTabs: [{
					name: '1'
				},{
					name: '1'
				},{
					name: '1'
				}],
				title: '素胚勾勒出青花，笔锋浓转淡',
				subTitle: '2020-05-15',
				thumb: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg',
				value1: 1,
				value2: 2,
				options1: [{
						label: '默认排序',
						value: 1,
					},
					{
						label: '距离优先',
						value: 2,
					},
					{
						label: '价格优先',
						value: 3,
					}
				]
			}
		},
		onLoad() {
			[1, 2, 3, 4, 5, 6, 7].map(item => {
				this.tabs.push({
					name: '木棉',
					desc: '木棉（学名：Bombax ceiba L.）是木棉科、木棉属落叶大乔木，树皮灰白色，幼树的树干通常有圆锥状的粗刺；分枝平展。掌状复叶，小叶5-7片，长圆形至长圆状披针形，花单生枝顶叶腋，通常红色，有时橙红色，直径约10厘米；萼杯状，长2-3厘米，外面无毛，内面密被淡黄色短绢毛，萼齿3-5，半圆形，花瓣肉质，倒卵状长圆形，蒴果长圆形'
				})
			})

		},
		methods: {
			// tabs通知swiper切换
			tabsChange(index) {
				this.swiperCurrent = index;
			},
			// swiper-item左右移动，通知tabs的滑块跟随移动
			transition(e) {
				let dx = e.detail.dx;
				this.$refs.uTabs.setDx(dx);
			},
			// 由于swiper的内部机制问题，快速切换swiper不会触发dx的连续变化，需要在结束时重置状态
			// swiper滑动结束，分别设置tabs和swiper的状态
			animationfinish(e) {
				let current = e.detail.current;
				this.$refs.uTabs.setFinishCurrent(current);
				this.swiperCurrent = current;
				this.current = current;
			},
			// scroll-view到底部加载更多
			onreachBottom() {

			}
		}
	}
</script>

<style scoped lang="scss">
	.u-card-wrap { 
		background-color: $u-bg-color;
		padding: 1px;
	}
	
	.u-body-item {
		font-size: 32rpx;
		color: #333;
		padding: 20rpx 10rpx;
	}
		
	.u-body-item image {
		width: 120rpx;
		flex: 0 0 120rpx;
		height: 120rpx;
		border-radius: 8rpx;
		margin-left: 12rpx;
	}
	::v-deep .u-dropdown__content {
		z-index: 2 !important;
	}
</style>
