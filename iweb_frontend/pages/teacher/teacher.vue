<template>
	<view>
	<view class="header">
		<view class="title">金牌讲师</view>
	</view>
	<uni-list>
		<view v-for="(t,i) in teacherList" :key="i" @click="doCourseClick(t.tid)">
			<view class="course">
				<image class="tpic" :src="server.host+t.tpic" mode=""></image>
				<view class="details">
					<view class="tname">{{t.tname}}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{{t.maincourse}}</view>
					<view class="experience">工作经历</view>
					<view class="experience-item" v-html="t.experience"><{{t.experience}}</view>
					<view class="style">授课风格</view>
					<view class="style-item">{{t.style}}</view>
				</view>
			</view>
		</view>
		
	</uni-list>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				teacherList:[],
			};
		},
		onLoad(options){
			uni.request({
				url:this.server.teacherList(),
				success:res=>{
					console.log(res.data)
					this.teacherList=res.data
				}
			})
		},
		methods:{
			doCourseClick(tid){
				
				uni.navigateTo({
					url:'/pages/teacherDetail/teacherDetail?tid='+tid
				})
			}
		}
	}
</script>

<style lang="scss">

.header{
		display: flex;
		// flex-direction: row;
		margin: 5rpx 0rpx 20rpx ;
		border-bottom: 1px solid $uni-border-color;
		.title{
			font-size: $uni-font-size-title;
			color:$iweb-theme-color;
			padding: 15rpx 35rpx;
			border-bottom: 1rpx solid $iweb-theme-color;
			transform: translateY(1rpx);
			font-weight: bold;
		}
		}
		.course{
			display: flex;
			// align-items: center;
			padding:10rpx 10rpx 40rpx;
			border-bottom:1rpx solid $uni-border-color;
			float: right;
			width: 95%;
			.tpic{
				width: 100px;
				height: 150px;
				// width: 100%;
			}
			.details{
				flex:1;
				padding-left:20rpx;
			overflow: hidden;
				.tname{
				 			color:$iweb-theme-color-reverse;
				 			font-weight: bold;
				 			margin-bottom: $uni-spacing-row-base;
				 		}
				.experience{
					font-weight: bold;
					}
				.experience-item{
					font-size: $uni-font-size-lg;
					padding-top:10rpx;
				}
				.style{
					font-weight: bold;
					padding-top:20rpx;
				}
				.style-item{
					font-size: $uni-font-size-lg;
					padding-top:10rpx;
				}
			}
		}
// .course{
// 	display: flex;
// 	align-items: center;
// 	padding:10px 10px;
// 	border-bottom: 1px solid $uni-border-color;
// 	float: right;
// 	width: 95%;
// 	image{
// 		width:100%;
// 	}
// 	.pic{
// 		// width:250rpx;
// 	}
// 	.details{
// 		flex:1;
// 		padding-left: 2rpx;
// 		overflow: hidden;
// 		.tname,.maincourse{
// 			color:$iweb-theme-color-reverse;
// 			font-weight: bold;
// 			margin-bottom: $uni-spacing-row-base;
// 		}
// 		// .sname{
// 		// 	font-size: $uni-font-size-lg;
// 		// 	font-weight:bold;
// 		// 	margin-bottom: $uni-spacing-row-base;
// 		// 	white-space: nowrap;
// 		// 	text-overflow: ellipsis;
// 		// 	overflow:hidden;
// 		// }
// 		.address,.phone,.postcode{
// 			font-size: $uni-font-size-base;
// 			color:$uni-text-color-grey;
// 		}
// 	}
// }
// image{
// 	width:100%;
// }
</style>
