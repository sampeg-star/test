<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},
		methods:{
			login:function(){
				var that = this;
				var code = '';
				wx.login({
					success: function(res) {
						console.log(res);
						if (res.code) {
							code = res.code;
							console.log('code',code);
						} else {}
					}
				});
				wx.getUserProfile({
					desc: '用于完善用户资料',
					success:(res)=>{
						console.log("getUserInfo:success", res);
						var code1 = code;
						console.log("1",code1)
					uni.request({
						url: "https://test.chudaikeji.com/proj-wxs-yxhh-zp/web/index.php/api/passport/login",
						method: "POST",
						header: {
							'content-type': 'application/x-www-form-urlencoded'
						},
						data: {
							code: code1,
							user_info:res.rawData,
							encrypted_data: res.encryptedData,
							iv: res.iv,
							signature:res.signature
							
						},
						success: function(res) {
							console.log(res)
							// let is_login = true;
							uni.setStorageSync('nickname',res.data.data.nickname)
							uni.setStorageSync('avatar_url',res.data.data.avatar_url)
							// uni.setStorageSync('login',is_login)
							uni.reLaunch({
								url:'../zhuce/zhuce'
							})
						},
						fail:function(res){
							console.log('error',res)
						}
					});
					}
				})
			},
			// request: function(object) {
			// 	let that = this;
			// 	wx.request({
			// 		url: object.url,
			// 		header: object.header || {
			// 			'content-type': 'application/x-www-form-urlencoded'
			// 		},
			// 		data: object.data || {},
			// 		method: object.method || "GET",
			// 		dataType: object.dataType || "json",
			// 		success: function(res) {
			// 			console.log(res);
			// 			wx.setStorageSync('user_id', res);
			// 		},
			// 		fail: function(res) {
			// 			wx.showToast({
			// 				icon: 'none',
			// 				title: '网络请求出错'
			// 			})
			// 		},
			// 		complete: function(res) {
			// 			if (object.complete) object.complete(res);
			// 		}
			// 	});
			// },
		}
	}
</script>

<style>
/* #ifdef APP-PLUS ||MP-WEIXIN */
		checkbox .wx-checkbox-input {
			border-radius: 50% !important;
			/* color: #ffffff !important; */
		}
	
		checkbox .wx-checkbox-input.wx-checkbox-input-checked {
			color: #fff;
			background: #ff0000;
		}
	
		/* .wx-checkbox-input.wx-checkbox-input-checked {
			border: none !important;
		} */
	
/* #endif */

	/*每个页面公共css */
</style>
