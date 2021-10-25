<script>
	export default {
		globalData: {
            loginInfo: {
				account: '张三',
				name: '张三公司'
			}
		},
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	.common {
		color: #4CD964;
	}
</style>
