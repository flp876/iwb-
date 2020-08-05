<template>
	<view class="container">
		
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// schoolCourse,
			};
		},
		onLoad(options){
			console.log('school course onload:',options)
			let sid=options.sid
			// #ifdef H5
			if(!sid){
				uni.showModal({
					title:'警告',
					content:'请从课程列表页进入当前页面！点击“确定”按钮返回列表页。',
					showCancel:false,
					success:res=>{
						console.log(res)
						uni.redirectTo({
							url:'/pages/school/school'
						})
						return
					}
				})
			}
			// #endif
			
			uni.showLoading({
				title:'加载中'
			})
			
			uni .request({
				// url:this.server.schoolCourse(sid),
				success:res=>{
					console.log(res.data)
					this.school=res.data
					uni.hideLoading()
				}
			})
		},
	}
</script>

<style lang="scss">

</style>
