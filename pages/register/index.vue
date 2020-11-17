<template>
	<view class="container">
		<u-form :model="form" ref="uForm" :rules="rules">
			<u-form-item label="账户" prop="username">
				<u-input type="text" placeholder="请输入账户" v-model="form.username" />
			</u-form-item>
			<u-form-item label="密码" prop="password">
				<u-input type="password" placeholder="请输入密码" v-model="form.password" />
			</u-form-item>
			<view class="loginBtn">
				<u-button type="primary" @click="submit">登录</u-button>
			</view>
		</u-form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				form: {
					username: '',
					password: ''
				},
				rules: {
					username: [
						{ 
							required: true, 
							message: '请输入账户', 
							// 可以单个或者同时写两个触发验证方式 
							trigger: ['change','blur']
						}
					],
					password: [
						{
							required: true,
							message: '请输入密码', 
							// 可以单个或者同时写两个触发验证方式 
							trigger: ['change','blur']
						}
					]
				}
			}
		},
		onReady() {
			this.$refs.uForm.setRules(this.rules);
		},
		methods: {
			submit() {
				this.$refs.uForm.validate(valid => {
					if (valid) {
						uni.showLoading({
							title: '注册中...'
						})
						uniCloud.callFunction({
							name: 'add',
							data: {
								username: this.form.username,
								password: this.form.password
							}
						}).then((res) => {
							uni.hideLoading()
							console.log(res)
						}).catch((err) => {
							uni.hideLoading()
							console.error(err)
						})
						
						uniCloud.callFunction({
							name: 'get'
						}).then((res) => {
							uni.hideLoading()
							uni.showModal({
								content: `查询成功，获取数据列表为：${JSON.stringify(res.result.data)}`,
								showCancel: false
							})
							console.log(res)
						}).catch((err) => {
							uni.hideLoading()
							uni.showModal({
								content: `查询失败，错误信息为：${err.message}`,
								showCancel: false
							})
							console.error(err)
						})
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.container{
		padding: 20rpx;
		
		.loginBtn{
			margin-top: 200rpx;
		}
	}
</style>
