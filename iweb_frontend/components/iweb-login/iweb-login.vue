<template>
	<view>
		<uni-card title="用户登录" is-shadow>
			<!-- UNI-APP中的双向数据绑定语法与Vue.js相同：v-model指令-->
			<input class="input" type="text" v-model="uname" placeholder="请输入用户邮箱" />
			<input class="input" type="text" v-model="upwd" placeholder="请输入登录密码" password/>
			<button class="button" @click="doLogin">登录</button>
			<view class="gotoRegister" @click="gotoRegister">注册新用户</view>
		</uni-card>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				uname:'ranran@tedu.cn',
				upwd: '123456'
			};
		},
		methods:{
			doLogin(){
				let data={
					uname:this.uname,
					upwd:this.upwd
				}
				uni.request({
					method:'POST',
					url:this.server.userLogin(),
					data:data,
					withCredentials:true,
					success:res=>{
						let body=res.data
						// console.log(body)
						if(body.code===200){
							uni.showToast({
								title:'登陆成功'
							})
							//在客户端持续的保留登陆状态即使刷新浏览器仍然可以读到登陆状态
							// getApp().globalData.userInfo=body.userInfo
							uni.setStorage({
								key:'userInfo',
								data:body.userInfo,
								success:()=>{
									this.$emit('loginComplete')
								}
							})
							
						}else{
							uni.showModal({
								title:'错误',
								content:'登陆失败！:' +body.code+'错误消息' ,
								showCancel:false
							})
						}
					}
				})
			},
			gotoRegister(){
				//子组件想修改父组件的数据——通过发射自定义事件
				this.$emit('requestShowRegister')
			},
		}
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
	.gotoRegister {
		text-align: right;
		color: $iweb-theme-color
	}
</style>
