<template>
	<view class="com-table">
		<view class="fixed-table" :style="{width: thWidth}">
			<view class="fixed-content" :style="{width: contentWidth}">
				<view
					class="item-tr" 
					v-for="(item, i) in titleData"
					:key="i"
				>
					<view
						class="item-title"
						:style="{flexBasis: thWidth}"
					>
						{{item.title}}
					</view>
					<view 
						class="item-td"
						v-for="(subItem, si) in tableData"
						:key="si"
					>
						{{subItem[item.key]}}
					</view>
				</view>
			</view>
	
		</view>
		<view class="scroll-box" :style="{left: thWidth, width: `calc(100% - ${thWidth})`}">
			<scroll-view class="scroll-view" scroll-x="true">
				<view class="scroll-table" :style="{width: scrollWidth}">
					<view
						class="item-tr" 
						v-for="(item, i) in titleData"
						:key="i"
					>
						<view 
							class="item-td"
							v-for="(subItem, si) in tableData"
							:key="si"
						>
							{{subItem[item.key]}}
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
		
	</view>
</template>

<script>
	export default {
		name: 'ComTable',
		props: {
			titleData: { // 标题对象数组 title表头 key取值key
				type: Array,
				default: () => []
			},
			tableData: { // 表格数据
				type: Array,
				default: () => []
			},
			titleWidth: { // 表头宽度
				type: Number,
				default: 90
			},
			width: {
				type: Number, // 表格宽度
				default: 70
			}
		},
		data() {
			return {
				contentWidth: '440px', // 表格宽度
				scrollWidth: '350px' ,// 滚动部分宽度
				thWidth: '90px' // 表头宽度
			}
		},
		watch: {
			tableData: function(val) {
				if (val && val.length){
					const leg = val.length
					this.thWidth = this.titleWidth + 'px'
					this.scrollWidth = this.width * leg + 'px'
					this.contentWidth = this.width * leg + this.titleWidth + 'px'
					console.log(this.thWidth, this.scrollWidth, this.contentWidth)
				}
			}
		},
		created() {
			console.log(999)
			if (this.tableData && this.tableData.length){
				const leg = this.tableData.length
				this.thWidth = this.titleWidth + 'px'
				this.scrollWidth = this.width * leg + 'px'
				this.contentWidth = this.width * leg + this.titleWidth + 'px'
				console.log(this.thWidth, this.scrollWidth, this.contentWidth)
			}

		}
	}
</script>

<style lang="scss" scoped>
	.com-table {
		margin-top: 20rpx;
		position: relative;
		.fixed-table {
			overflow: hidden;
			border: 2rpx solid #e4e7ed;
			border-top: none;
		}
		.item-tr {
			display: flex;
			line-height: 60rpx;
			.item-title {
				border-right: 2rpx solid #e4e7ed;
				border-top: 2rpx solid #e4e7ed;
				background-color: #f5f6f8;
				padding-left: 20rpx;
				background-color: #f5f7fa;
			}
			.item-td {
				flex: 1;
				padding-left: 20rpx;
				border-right: 2rpx solid #e4e7ed;
				border-top: 2rpx solid #e4e7ed;
			}
		}
		.scroll-box {
			position: absolute;
			top: 0;
			.scroll-view {
				.scroll-table {
					border-bottom: 2rpx solid #e4e7ed;
					border-left: 2rpx solid #e4e7ed;
				}
			}
		}
	}
</style>
