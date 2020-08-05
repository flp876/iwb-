<template>
	<view class="user">
		<block v-if="user.uid">
			<image class="avatar" :src="server.host + user.avatar" mode="scaleToFill" />
			<uni-collapse accordion>
				<uni-collapse-item title="我的信息" open>
					<view class="pane">
						<view class="row">
							<view class="label">用户:</view>
							<view >{{user.uname}}</view>
						</view>
						<view class="row">
							<view class="label">昵称:</view>
							<view >{{user.nickname}}</view>
						</view>
						<view class="row">
							<view class="label">电话:</view>
							<view >{{user.phone | phoneMask}}</view>
						</view>
						<view class="row">
							<view class="label">性别:</view>
							<view >{{user.sex}}</view>
						</view>
					</view>
				</uni-collapse-item>
				<uni-collapse-item title="修改密码">
					<view class="pane">
						<view class="pane">
							<button @click="chooseUploadUpdateAvatat">选择上传头像</button>
						</view>
					</view>
				</uni-collapse-item>
				<uni-collapse-item title="修改头像">
					<view class="pane">
						
					</view>
				</uni-collapse-item>
				<uni-collapse-item title="我的订单">
					<view class="pane">
						
					</view>
				</uni-collapse-item>
				<uni-collapse-item title="我的收藏夹">
					<view class="pane">
						
					</view>
				</uni-collapse-item>
			</uni-collapse>
		</block>
		<view class="loading" v-else>
			用户数据加载中...
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				user:{},
			};
		},
		mounted(){
			uni.request({
				url:this.server.userDetails(),
				withCredentials:true,
				success:res=>{
					 this.user=res.data,
					console.log(this.user)
				}
			})
		},
	methods:{
		chooseUploadUpdateAvatat(){
		   	uni.chooseImage({
		   		count:1,
				success:result=>{
					// console.log(result)
					let file=result.tempFiles[0]
				}
		   	})
		}
	},
	}
</script>

<style lang="scss">
    .user{
		// padding:
		.avatar{
			width: 140rpx;
			height: 140rpx;
			display: block;
			margin: 20rpx auto;
			border-radius: 50%;
			box-shadow: 0 0 8rpx #888;
		}
		.pane{
			padding: 20rpx 20rpx 40rpx;
			background: lighten($uni-bg-color-grey,1);
			.row{
				line-height: 1.6em;
				display: flex;
				.label{
					font-weight: bold;
					margin-right:1em;
				}
			}
		}
		.loading{
			text-align: center;
			margin: 50rpx 0;
		}
	}
</style>
