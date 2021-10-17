<template>
	<view class="detail">
		<view>详情页{{title}}</view>
		<text selectable>可选择的文本</text>
		<view>
			<text selectable space="ensp">唱歌 跳舞</text>
		</view>
		<view>
			<text selectable space="emsp">唱歌 跳舞</text>
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return {
				title: 'test'
			}
		},
		 onLoad: function (option) { //option为object类型，会序列化上个页面传递的参数
			console.log(option.id); //打印出上个页面传递的参数。
			console.log(option); //打印出上个页面传递的参数。
		}
	}
</script>

<style>
</style>
