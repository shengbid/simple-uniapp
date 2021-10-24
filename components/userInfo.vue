<template>
	<view>
		子组件
		<view class="title">
			姓名: {{userInfo.name}}
		</view>
		<view class="title">
			年龄: {{userInfo.age}}
		</view>
		<button @click="clickName">改变名字</button>
	</view>
</template>

<script>
	export default {
		name:"userInfo",
		props: {
			userInfo: {
				type: Object,
				default: () => {return {}}
			}
		},
		data() {
			return {
				count: 1
			};
		},
		created() {
		},
		methods: {
			clickName() {
				this.$emit('changeName', `张三${this.count++}`)
			}
		}
	}
</script>

<style>

</style>
