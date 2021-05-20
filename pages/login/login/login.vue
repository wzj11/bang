<template>
	<view>
		<view class="title">
			登录
		</view>
		<view class="dotted"></view>
		<view class="cu-form-group">
			<view class="name">手机号:</view>
			<input placeholder="请输入手机号" focus="true" v-model="phone" type="number" maxlength="11" name="input"></input>
			<button class='cu-btn bg-orange text-white' :style="disabled ? 'color: #000000;' : ''" :disabled="disabled"
				@click="getCount">{{!second?'获取验证码':second+'s重新获取'}}</button>
		</view>
		<view class="dotted"></view>
		<view class="cu-form-group">
			<view class="name">验证码:</view>
			<input placeholder="请输入验证码" v-model="code" type="number" maxlength="6" name="input"></input>
		</view>
		<view class="dotted"></view>
		<view class="padding flex flex-direction">
			<button class="cu-btn bg-orange margin-tb-sm lg text-white" :style="showdisabled ? 'color: #000000;' : ''"
				:disabled="showdisabled" @click="logPut">提交</button>
			<button class="cu-btn bg-orange margin-tb-sm lg text-white" open-type="getUserInfo"
				@getuserinfo="getUserInfo">微信授权登录（open-type 获取）</button>
			<button class="cu-btn bg-orange margin-tb-sm lg text-white" open-type="getPhoneNumber"
				@getphonenumber="getUserPhone">微信手机号登录</button>
			<button class="cu-btn bg-orange margin-tb-sm lg text-white" open-type="contact">联系客服</button>
			<!-- 最新版微信登录测试 -->
			<button class="cu-btn bg-orange margin-tb-sm lg text-white" @tap="goLogin">最新版微信登录测试（按钮直接登录）</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 手机号
				phone: '',
				// 验证码
				code: '',
				//验证码倒计时
				second: 0,
				disabled: true,
			}
		},
		computed: {
			showdisabled() {
				return !!!this.phone || !!!this.code
			}
		},
		onLoad() {
			this.goLogin()
		},
		methods: {
			// 提交
			logPut() {
				this.$operate.toast({
					title: '登录成功'
				})
			},
			// 验证码倒计时
			getCount() {
				this.disabled = true
				this.second = 60
				let timer = setInterval(() => {
					this.second--;
					if (this.second < 1) {
						clearInterval(timer);
						this.disabled = false
						this.second = 0
					}
				}, 1000)
			},
			//获取用户授权  匿名数据
			getUserInfo(e) {
				if (e.detail.errMsg == 'getUserInfo:ok') {
					//对数据进行操作
					console.log(e)
				} else {
					this.$operate.toast({
						title: '授权失败无法登录！'
					})
				}
			},
			// 获取用户信息  后期放弃
			userInfo() {
				uni.login({
					provider: 'weixin',
					success(login) {
						console.log(login);
						uni.getUserInfo({
							provider: 'weixin',
							lang: 'zh_CN',
							success(user) {
								console.log(user);
							}
						})
					}
				})
			},
			//获取用户手机号
			getUserPhone(e) {
				// 获取code 小程序专有，用户登录凭证。
				uni.login({
					provider: 'weixin',
					success(login) {
						console.log(login);
					}
				})
				//手机号加密数据
				if (e.detail.errMsg == 'getPhoneNumber:ok') {
					console.log(e)
					//传给后端的参数
					let data = {
						session_key: '后端返回微信 openid ',
						encryptedData: e.detail.encryptedData,
						iv: e.detail.iv,
					}
					
				} else {
					this.$operate.toast({
						title: '授权失败无法登录！'
					})
				}
			},
			//最新登录测试
			goLogin() {
				// 获取code 小程序专有，用户登录凭证。
				uni.login({
					provider: 'weixin',
					success(login) {
						console.log(login);
					}
				})
				 // desc: '用于完善会员资料'  必填 声明获取用户个人信息后的用途，后续会展示在弹窗中
				uni.getUserProfile({
					desc: '用于完善会员资料',
					lang: 'zh_CN',
					success(user) {
						console.log(user);
					}
				})
			},
			//监听 手机号输入
			import() {
				if (this.phone.length != 0) {
					this.disabled = false
					return;
				}
				this.disabled = true;
			},
		},
		watch: {
			phone(val) {
				this.import()
			}
		}
	}
</script>

<style lang="scss">
	page {
		background-color: #FFFFFF;
	}

	.title {
		margin-top: 20rpx;
		text-align: center;
		color: #333333;
		font-size: 35rpx;
		margin-bottom: 20rpx;
	}

	.dotted {
		height: 1rpx;
		width: 100%;
		margin: 10rpx 0;
		background-color: #f4f4f4;
	}

	.login {
		margin: 20rpx;
		background-color: #007AFF;
		height: 200rpx;

	}

	.name {
		color: #333333;
		font-size: 30rpx;
		margin-right: 15rpx;
	}
</style>