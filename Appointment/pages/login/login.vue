<template>
	<view class="after-navber">
	  <view style="padding: 0 60rpx">
	    <view style="padding:80rpx 0 48rpx;border-bottom: 1rpx solid #e3e3e3;margin-bottom: 72rpx;text-align: center">
	    <!--  <image src="../../static/check.png" style="width: 200rpx;height: 200rpx;"></image> -->
	    </view>
	    <view style="font-size: 13pt;margin-bottom: 40rpx">申请获取以下权限</view>
	    <view style="color: #888;margin-bottom: 88rpx">获得你的公开信息（昵称、头像等）</view>
		<button class="login-btn" @tap="getUserProfile"> 获取头像昵称 </button>
	  </view>
	</view>
</template>

<script>
	var app = getApp();
	export default {
	  data() {
	    return {
	      nickname:''
	    };
	  },
	  onLoad(){
	  },
	  methods:{
			  getUserProfile() {
			  let that = this;
			  app.login();
			  
		  }
	  }
	  }
</script>

<style lang="scss">
	body{ background: #fff; }
	.login-btn{ border: none; height: 88rpx; line-height: 88rpx; background: #04be01; color: #fff; font-size: 11pt; border-radius: 999rpx; }
	.login-btn::after{ display: none; }
	.login-btn.button-hover { box-shadow: inset 0 5rpx 30rpx rgba(0,0,0,.15); }
	
	/*按钮*/
	.loginBtnView {
	  width: 100%;
	  height: auto;
	  background-color: #f2f2f2;
	  margin-top: 0px;
	  margin-bottom: 0px;
	  padding-bottom: 0px;
	
	}
	.loginBtn {
	  width: 80%;
	  margin-top: 35px;
	}
</style>
