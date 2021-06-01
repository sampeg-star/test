<template>
	<view class="hyzxxf_content">
		<view class="hyzxxf_top">
			<view class="hyzxxf_user">
			<view class="user_img">
				<image :src="avatar_url" mode=""></image>
			</view>
			<view class="user_msg">
				<view class="user_msg_box">
					<image src="../../static/images/uservip.jpg" mode=""></image>
					<view class="user_vip">
						普通会员
					</view>
				</view>
				<view class="user_vip_time">
					您的会员将在{{time}}到期
				</view>
			</view>
			</view>
			<view class="vip_btn" @click="jump">
				续费
			</view>
		</view>
		<view class="hyzx_spatic">
			<view class="hyzx_spatic_title">
				<image src="../../static/images/ybr1.jpg" mode=""></image>
				<text>当前会员特权</text>
				<image src="../../static/images/ybl1.jpg" mode=""></image>
			</view>
			<view class="hyzx_nr">
				<view class="hyzx_tq_msg">
					<image src="../../static/images/ckxx1.jpg" mode=""></image>
					<image src="../../static/images/sfbz1.jpg" mode=""></image>
				</view>
				<view class="hyzx_tq_text">
					<text>查看详情信息</text>
					<text>会员身份标识</text>
				</view>
				<view class="hyzx_tq_text1">
					<view style="color: rgb(118, 118, 118);">免费查看会员详情信息</view>
					<view style="color: rgb(118, 118, 118);">
						身份加
						<image src="../../static/images/sfbz1.jpg" mode=""></image>
						标识吸引更多关注
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				nickname:'',
				avatar_url:'',
				time:''
			}
		},
		onLoad() {
			this.nickname = uni.getStorageSync('nickname');
			this.avatar_url = uni.getStorageSync('avatar_url');
			if(this.nickname == ""){
				uni.navigateTo({
					url:'../login/login'
				})
			};
			let data = new Date();
			let y = data.getFullYear();
			let m = data.getMonth() + 1;
			let d = data.getDate();
			if(m < 10){
				m = "0" + m;
			}
			this.time = y + "-" + m + "-" + d;
		},
		methods:{
			jump(){
				uni.navigateTo({
					url:'../hyzx/hyzx'
				})
			}
		}
	}
</script>

<style lang="scss">
	page{
		background-color: #F1F1F1;
	}
	@import '/hyzxxf.scss';
</style>
