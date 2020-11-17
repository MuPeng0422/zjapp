<template>
	<view class="container">
		<view class="banner">
			<u-image width="100%" height="300rpx" :src="src"></u-image>
		</view>
		<view class="title">
			火灾调查
		</view>
		<view class="form">
			<u-form :model="form" ref="uForm" :rules="rules">
				<u-form-item label="账户" prop="username"><u-input type="text" v-model="form.username" /></u-form-item>
				<u-form-item label="密码" prop="password"><u-input type="password" v-model="form.password" /></u-form-item>
			</u-form>
			<view class="loginBtn">
				<u-button type="primary" @click="submit">登录</u-button>
			</view>
			<view class="editpassword">
				<view class="" @click="editpwd">
					忘记密码？
				</view>
				<view class="" @click="register">
					没有账号？<span>立即注册</span>
				</view>
			</view>
		</view>
		<u-toast ref="uToast" />
	</view>
</template>

<script>
	export default {
		data() {
			return {
				src: 'https://cdn.uviewui.com/uview/example/fade.jpg',
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
						console.log('123456')
						uniCloud.callFunction({
							name: 'get'
						}).then((res) => {
							uni.hideLoading()
							console.log(res)
						}).catch((err) => {
							uni.hideLoading()
							console.error(err)
						})
						// if (this.form.username !== loginData.data.username) {
						// 	this.$refs.uToast.show({
						// 		title: '账户错误',
						// 		type: 'error'
						// 	})
						// 	return false;
						// }
						
						// if (this.form.password !== loginData.data.password) {
						// 	this.$refs.uToast.show({
						// 		title: '密码错误',
						// 		type: 'error'
						// 	})
						// 	return false;
						// }
						console.log('123456')
						this.$u.route('/pages/index/index');
					} else {
						console.log('验证失败');
					}
				});
			},
			editpwd() {
				this.$u.route('/pages/editpassword/index')
			},
			register() {
				this.$u.route('/pages/register/index')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.title{
		font-size: 60rpx;
		padding: 50rpx;
		text-align: center;
	}
	
	.form{
		margin: 0 auto;
		padding: 50rpx;
		background-color: #FFFFFF;
		
		.loginBtn{
			margin: 50rpx auto;
		}
		
		.editpassword{
			display: flex;
			justify-content: space-between;
			
			span{
				text-decoration: underline;
				color: #007AFF;
			}
		}
	}
</style>
