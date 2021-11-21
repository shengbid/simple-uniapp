<template>
	<view class="table-box">
		<view class="title">
			纵向table
		</view>
		<view class="test">
			<scroll-view scroll-x="true">
			<view class="text">
				<view class="txt">
					55555555
					<view class="t">
						8888
					</view>
				</view>
				<view class="txt">
					55555555
				</view>
				<view class="txt">
					55555555
				</view>
				<view class="txt">
					55555555
				</view>
				<view class="txt">
					55555555
				</view>
			</view>
			</scroll-view>
		</view>
		<view class="table">
			<view class="fixed-table" :style="{width: titleWidth}">
				<view class="fixed-content" :style="{width: width}">
					<view
						class="item-tr" 
						v-for="(item, i) in titleData"
						:key="i"
					>
						<view
							class="item-title"
							:style="{flexBasis: titleWidth}"
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
			<view class="scroll-box" :style="{left: titleWidth, width: `calc(100% - ${titleWidth})`}">
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

		<com-table :tableData="tableData" :titleData="titleData">
			
		</com-table>
	</view>
</template>

<script>
	import ComTable from '@/components/ComTable'
	export default{
		components: {
			ComTable
		},
		data(){
			return {
				titleData: [
					{title: '学校', key: 'name'}, 
					{title: '班级', key: 'class'},
					{title: '年龄', key: 'age'}
				],
				titleWidth: '90px',
				width: '600px',
				scrollWidth: '510px',
				tableData: [
					{name: '浙江大学', class: '二年级', age: 20},
					{name: '深圳大学', class: '二年级', age: 20},
					{name: '东北下下大学', class: '二年级', age: 20},
					{name: '浙江大学', class: '二年级', age: 20},
				]
			}
		},
		onShow() {
			console.log(33)
			setTimeout(()=> {
					this.tableData.push(
						{name: '浙江', class: '二年级', age: 20},
						{name: '浙江大学', class: '二年级', age: 20},
						{name: '浙江大学', class: '二年级', age: 20}
					)
			}, 300)
		}
	}
</script>

<style lang="scss">
	.title {
		border: 1px solid #e4e7ed;
	}
	.table-box {
		padding: 30rpx;
	}
	.table {
		margin-top: 10px;
		position: relative;
		.fixed-table {
			overflow: hidden;
			border: 1px solid #e4e7ed;
			border-top: none;
		}
		.item-tr {
			display: flex;
			line-height: 30px;
			.item-title {
				border-right: 1px solid #e4e7ed;
				border-top: 1px solid #e4e7ed;
				background-color: #f5f6f8;
				padding-left: 10px;
				background-color: #f5f7fa;
			}
			.item-td {
				flex: 1;
				padding-left: 10px;
				border-right: 1px solid #e4e7ed;
				border-top: 1px solid #e4e7ed;
			}
		}
		.scroll-box {
			position: absolute;
			top: 0;
			.scroll-view {
				.scroll-table {
					border-bottom: 1px solid #e4e7ed;
					border-left: 1px solid #e4e7ed;
				}
			}
		}
	}
	
	.test {
		
		width: 100%;
		.text {
			display: flex;
			
			background-color: #00C800;
			
			.txt {
				flex: 1;
				border: 1px solid #fff;
				padding: 10rpx;
			}
		}
	}

</style>
