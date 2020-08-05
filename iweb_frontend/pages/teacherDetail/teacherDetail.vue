<template>
	<view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// teacherDetail,
			};
		},
		onLoad(options){
			console.log('teacher detail onload:',options)
			let tid=options.tid
			// #ifdef H5
			if(!tid){
				uni.showModal({
					title:'警告',
					content:'请从课程列表页进入当前页面！点击“确定”按钮返回列表页。',
					showCancel:false,
					success:res=>{
						console.log(res)
						uni.redirectTo({
							url:'/pages/teacher/teacher'
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
				url:this.server.teacherDetail(tid),
				success:res=>{
					console.log(res.data)
					this.teacher=res.data
					uni.hideLoading()
				}
			})
		},
	}
</script>

<style lang="scss">

</style>
