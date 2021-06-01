<template>
	<view class="user_content">
		<view class="user_bj">
		<view class="user_msg">
			<view class="user_photo">
				<image src="../../static/images/tx3.jpg" mode="" v-if="avatar_url == ''"></image>
				<image :src="avatar_url" mode="" v-else></image>
			</view>
			<view class="user_tx">
				<view class="user_name" v-if="nickname == ''">
					明天更好
				</view>
				<view class="user_name" v-else>
					{{nickname}}
				</view>
				<view class="user_level">
					<text>我的等级:</text>
					<image src="../../static/images/dj.jpg" mode=""></image>
				</view>
			</view>
		</view>
		</view>
		
		<view class="user_choose">
			<view class="user_jb" @click="jump1">
				<image src="../../static/images/jbzl.jpg" mode=""></image>
				<text>基本资料</text>
			</view>
			<view class="user_cz" @click="jump3">
				<image src="../../static/images/czhd.jpg" mode=""></image>
				<text>充值活动</text>
			</view>
			<view class="user_bm" @click="jump2">
				<image src="../../static/images/wdbm.jpg" mode=""></image>
				<text>我的报名</text>
			</view>
			<view class="user_hy" @click="jump4">
				<image src="../../static/images/wdhy.jpg" mode=""></image>
				<text>我的会员</text>
			</view>
		</view>
		<view class="user_choose1">
			<view class="user_jl" @click="jump">
				<view>
				<image src="../../static/images/lljl.jpg" mode=""></image>
				<text>浏览记录</text>	
				</view>
				<image src="../../static/images/arrowright.jpg" style="width: 30rpx;height: 30rpx;" mode=""></image>
			</view>
			<view class="user_gz" @click="jump5">
				<view>
					<image src="../../static/images/wdgz.jpg" mode=""></image>
					<text>我的关注</text>
				</view>
				<image src="../../static/images/arrowright.jpg" style="width: 30rpx;height: 30rpx;" mode=""></image>
			</view>
			<view class="user_dhkf" @click="call()">
				<view>
					<image src="../../static/images/dhkf.jpg" mode=""></image>
					<text>电话客服</text>
				</view>
				<image src="../../static/images/arrowright.jpg" style="width: 30rpx;height: 30rpx;" mode=""></image>
			</view>
			<view class="user_wxkf">
				<button type="default" open-type="contact" ><image src="../../static/images/wxkf.jpg" mode=""></image><text>微信客服</text><image src="../../static/images/arrowright.jpg" style="width: 30rpx;height: 30rpx; position: absolute; right: 0rpx;" mode=""></image></button>
			</view>
			<view class="user_gywm">
				<view>
				<image src="../../static/images/gywm.jpg" mode=""></image>
				<text>关于我们</text>	
				</view>
				
				<image src="../../static/images/arrowright.jpg" style="width: 30rpx;height: 30rpx;" mode=""></image>
			</view>
		</view>
	</view>
</template>

<script>
	const app = getApp();
	export default {
		data() {
			return {
				nickname:'',
				avatar_url:''
			}
		},
		onLoad() {
			this.nickname = uni.getStorageSync('nickname');
			let list = uni.getStorageSync('list')
			if(list.avatar == ''){
				this.avatar_url  = uni.getStorageSync('avatar_url');
			}else{
				this.avatar_url  = list.avatar
			}
			if(this.nickname == ""){
				uni.navigateTo({
					url:'../login/login'
				})
			}
		},
		methods: {
			getUserProfile() {
			let that = this;
			   app.login();
			 },
			jump(){
				var that = this;
				that.nickname = uni.getStorageSync('nickname');
				if(that.nickname != ''){
					uni.navigateTo({
					url:'../lljl/lljl'
					})
				}else{
					uni.navigateTo({
						url:'../login/login'
					})
				}
				
			},
			jump1(){
				var that = this;
				that.nickname = uni.getStorageSync('nickname');
				if(that.nickname != ''){
					uni.navigateTo({
						url:'../bjzl/bjzl'
					})
				}else{
					uni.navigateTo({
						url:'../login/login'
					})
				}
			},
			jump2(){
				var that = this;
				that.nickname = uni.getStorageSync('nickname');
				if(that.nickname != ''){
					uni.navigateTo({
						url:'../wdbm/wdbm'
					})
				}else{
					uni.navigateTo({
						url:'../login/login'
					})
				}
				
			},
			jump3(){
				var that = this;
				that.nickname = uni.getStorageSync('nickname');
				if(that.nickname != ''){
					uni.navigateTo({
						url:'../yecz/yecz'
					})
				}else{
					uni.navigateTo({
						url:'../login/login'
					})
				}
			},
			jump4(){
				var that = this;
				that.nickname = uni.getStorageSync('nickname');
				if(that.nickname != ''){
					uni.navigateTo({
						url:'../hyzxxf/hyzxxf'
					})
				}else{
					uni.navigateTo({
						url:'../login/login'
					})
				}
				
			},
			jump5(){
			var that = this;
			that.nickname = uni.getStorageSync('nickname');
			if(that.nickname != ''){
				uni.navigateTo({
				url:'../wdgz/wdgz'
				})
			}else{
				uni.navigateTo({
					url:'../login/login'
				})
			}
			},
			call(){
				uni.makePhoneCall({
				    phoneNumber: '114' //仅为示例
				});
			}
		}
	}
</script>

<style lang="scss">
	
	@import '/user.scss';
</style>
