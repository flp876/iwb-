<template>
	<view>
		<uni-card title="注册新用户" is-shadow>
			<!-- TODO: 此处在输入框失去焦点时，应该有客户端验证 -->
			<input class="input" type="text" v-model="uname" placeholder="请输入用户邮箱" />
			<input class="input" type="text" v-model="upwd" placeholder="请输入登录密码" password/>
			<input class="input" type="text" v-model="repwd" placeholder="请再次确认密码" password/>
			<input class="input" type="number" v-model="phone" placeholder="请输入电话号码" />
			<input class="input" type="text" v-model="captcha" maxlength="5" placeholder="请输入验证码" />
			<!-- 刷新验证码的原理：图片地址就是一个API地址，永远不变；变的是地址后追加的查询字符串 -->
			<image mode="widthFix" class="captcha" :src="server.captchaRegister()+'?'+rand" @click="rand=Math.random()"/>
			<button class="button" @click="doRegister">注册</button>
			<view class="gotoLogin" @click="gotoLogin">已经注册，开始登录</view>
		</uni-card>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				rand: Math.random(),
				uname: 'dongdong@tedu.cn',		//用户名，即邮箱
				upwd: '666666',					//密码
				repwd: '666666',				//确认密码
				phone: '13506666666',			//电话
				captcha: '',					//验证码
			};
		},
		methods:{
			doRegister(){	//完成用户注册
				let data = {	//注册数据
					uname: this.uname,
					upwd: this.upwd,
					phone: this.phone,
					captcha: this.captcha.toLowerCase()	//向服务器提交的验证码都是小写
				}
				//异步提交给服务器API，执行用户注册功能
				uni.request({
					method: 'POST',
					url: this.server.userRegister(),
					data: data,		//请求主体数据
					withCredentials: true,		//必需的！在请求头中携带身份认证信息(Cookie)
					//header: {'Content-Type': 'application/json'}  自定义的请求头部
					success: res=>{
						this.rand=Math.random()
						// console.log(res)
						let body=res.data
						if(body.code===200){
							uni.showModal({
								title:'成功',
								content:'新用户注册成功！点击‘确定’开始登陆。',
								showCancel:true,
								success:result=>{
									if(result.confirm){
										this.$emit('requestShowLogin')
									}
								}
							})
						}else{
							uni.showModal({
								title:'登陆失败',
								content:'新用户注册成功！点击‘确定’开始登陆。',
								showCancel:false,
								})
						}
					}
				})
			},
			gotoLogin(){
				//子组件想向父组件发射自定义事件，请求显示登录组件
				this.$emit('requestShowLogin')
			}
		},
	}
</script>

<style lang="scss">
	.input {
		height: 3.4em;
		padding: 0  20rpx;   //如果竖直方向上的padding值大于height，会导致无法获得焦点
		border-bottom: 1px solid $uni-border-color;
	}
	.button {
		margin:  30rpx 0;
	}
	.captcha {
		width: 100%;
		margin-top: 10rpx;
	}
	.gotoLogin {
		text-align: right;
		color: $iweb-theme-color
	}
</style>
