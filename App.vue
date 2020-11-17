<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
			uniCloud.callFunction({
				name:"get_list",
				data:{
					name: "wangyang",
					age:15
				},
				success(res) {
					console.log(res)
				},
				fail() {
					
				}
			})
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	/*每个页面公共css */
	@import "uview-ui/index.scss";
</style>
