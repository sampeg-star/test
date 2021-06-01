<template>
	<view class="sm_content">
		<view class="sm_box">
			协议内容协议内容协议内容
			协议内容协议内容协议内容
			协议内容协议内容协议内容协议内容
			协议内容协议内容协议内容协议内容
			协议内容v协议内容协议内容协议内容
			协议内容协议内容协议内容协议内容
			协议内容协议内容协议内容协议内容
			协议内容协议内容协议内容协议内容
		</view>
		<view class="sm_btn_box">
			<view class="sm_btn" @click="jump">
				确定
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				check:1
			}
		},
		methods:{
			
			jump(){
				let pages = getCurrentPages(); //获取所有页面栈实例列表
					let nowPage = pages[pages.length - 1]; //当前页页面实例
					let prevPage = pages[pages.length - 2]; //上一页页面实例
					prevPage.$vm.checked = this.check; //修改上一页data里面的tagIndex 参数值
					uni.navigateBack({ //uni.navigateTo跳转的返回，默认1为返回上一级
						delta: 1
					});
				// uni.navigateTo({
				// 	url:'../zhuce/zhuce?check=' + this.check
				// })
			}
		}
	}
</script>

<style lang="scss">
	page{
		padding-bottom: 150rpx;
		background-color: #F1F1F1;
	}
	@import '/sm.scss';
</style>
