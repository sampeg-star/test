<template>
	<view class="bkzl_content">
		<view class="bjzl_box" @click="chooseAvatar">
			<text>头像</text>
			<view class="bjzl_img">
				<image src="../../static/images/tx2.jpg" mode="aspectFill" v-if="avatar == ''"></image>
				<image :src="avatar" mode="aspectFill" v-else></image>
			<u-icon name="arrow-right"></u-icon>
			</view>
			<!-- <view class="wrap">
				<view class="u-avatar-wrap">
					<image class="u-avatar-demo" :src="avatar" mode="aspectFill"></image>
					<u-icon name="arrow-right"></u-icon>
				</view>
				
			</view> -->
		</view>
		<view class="bjzl_msg">
			<u-form :model="form" ref="uForm">
				<u-form-item label="民族" prop="mingzu">
					<!-- <u-input @click="show = true"  v-model="form.mingzu" type="select" placeholder-style="color:#ffffff"/> -->
					<view @click="show = true" style="width: 100%;display: flex;justify-content: space-between;">
						<text>{{form.mingzu}}</text>
						<u-icon name="arrow-right"></u-icon>
					</view>
				</u-form-item>
				<u-form-item label="学历" prop="xueli">
					<!-- <u-input  @click="xuelishow = true" v-model="form.xueli" type="select" placeholder-style="color:#ffffff"/> -->
					<view @click="xuelishow = true" style="width: 100%;display: flex;justify-content: space-between;">
						<text>{{form.xueli}}</text>
						<u-icon name="arrow-right"></u-icon>
					</view>
				</u-form-item>
				<u-form-item label="身高" prop="shengao">
					<u-input v-model="form.shengao" placeholder="请输入身高/cm" />
				</u-form-item>
				<u-form-item label="体重" prop="tizhong">
					<u-input v-model="form.tizhong" placeholder="请输入体重/kg" />
				</u-form-item>
			</u-form>
			<u-picker :range="actionSheetList" mode="selector" v-model="show" @confirm="actionSheetCallback"></u-picker>
			<u-picker :range="actionSheetList1" mode="selector" v-model="xuelishow" @confirm="actionSheetCallback1"></u-picker>
		</view>
		<view class="bjzl_msg1">
			<u-form :model="form" ref="uFor">
				<u-form-item label="收入" prop="shouru">
					<u-input v-model="form.shouru" placeholder="请输入您的收入" />
				</u-form-item>
				<u-form-item label="职业" prop="zhiye">
					<u-input v-model="form.zhiye" placeholder="请输入您的职业" />
				</u-form-item>
				<u-form-item label="居住地" label-width="130" prop="juzhudi">
					<!-- <u-input v-model="form.juzhudi" @click="juzhudishow = true" type="select" placeholder-style="color:#ffffff"/> -->
					<view @click="juzhudishow = true" style="width: 100%;display: flex;justify-content: space-between;">
						<text>{{form.juzhudi}}</text>
						<u-icon name="arrow-right"></u-icon>
					</view>
				</u-form-item>
				<u-picker :range="actionSheetList2" mode="region" v-model="juzhudishow" @confirm="actionSheetCallback2"></u-picker>
			</u-form>
		</view>
		<view class="bjzl_msg2">
			<view class="bjzl_msg2_title">
				自我条件(可多选)
			</view>
			<!-- <radio-group @change="radioChange">
				<label class="uni-list-cell uni-list-cell-pd" v-for="(item, index) in items" :key="item.value">
					<view class="bjzl_msg2_img">
						<image :src="item.pic" mode=""></image>
						<view>{{item.name}}</view>
					</view>

					<view>
						<radio color="red" style="transform:scale(0.7)" :value="item.value" :checked="index === current" />
					</view>

				</label>
			</radio-group> -->
			
			<checkbox-group >
			                <label @click="checkboxChange(item,$event)" :data-id="item.id" 
							class="uni-list-cell uni-list-cell-pd" v-for="item in items" :key="item.value">
			                    <view class="bjzl_msg2_img">
			                    	<image :src="item.pic" mode=""></image>
			                    	<view>{{item.name}}</view>
			                    </view>
								<view>
			                        <checkbox :value="item.value" :checked="item.checked"/>
			                    </view>
			                </label>
			</checkbox-group>
				
			
		</view>
		<view class="bjzl_msg3">
			<view class="bjzl_msg3_title">
				自我介绍
			</view>
			<u-input v-model="value" :type="type" :height="height" :auto-height="autoHeight" placeholder="请输入自我介绍" custom-style="{zIndex:-1}"/>
		</view>
		<view class="bjzl_msg4">
			<view class="bjzl_msg4_tilte">
				上传相册
			</view>
			<view class="image_choose">
				<u-upload ref="uUpload" :custom-btn="true" :action="action" max-count="6">
					<view slot="addBtn" class="slot-btn" hover-class="slot-btn__hover" hover-stay-time="150" style="width: 200rpx; height: 200rpx;margin: 5px; background-color: #eaeaea; border-radius: 20rpx;">
						<image mode="widthFix" src="../../static/images/write_repair_camera.png"></image>
					</view>
				</u-upload>
			</view>
		</view>
		<cover-view class="bjzl_btn_box" style="z-index: 99;">
			<cover-view class="bjzl_btn" @click.stop="submit" style="z-index: 999;" >
				<cover-image src="../../static/images/jbbj.png"></cover-image>
			<cover-view style="position: absolute;top: 50%;left: 50%;transform: translate(-50%,-50%);" >保存</cover-view>
			</cover-view>
		</cover-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				form: {
					mingzu: '',
					xueli: '',
					shengao: '',
					tizhong: '',
					juzhudi: '',
					shouru:'',
					zhiye:''
				},
				rules: { //表单验证
								
								shengao:[
									{
										pattern:/\d/,
										transform(value) {
											return String(value);
										},
										message: '请输入数字'
									}
									
								],
								
								tizhong:[
									
									{
										pattern:/\d/,
										transform(value) {
											return String(value);
										},
										message: '请输入数字'
									}
								],
								
								shouru:[
									{
										pattern:/\d/,
										transform(value) {
											return String(value);
										},
										message: '请输入数字'
									}
								],
								zhiye:[
									{
										pattern:/^[\u4e00-\u9fa5]+$/,
										transform(value) {
											return String(value);
										},
										message: '请输入文字'
									}
								],
							},
				value: '',
				type: 'textarea',
				height: 300,
				autoHeight: true,
				items: [{
						id:"1",
						value: 'room',
						name: '有房',
						pic: '../../static/images/yf.jpg',
						checked:false
					},
					{
						id:"2",
						value: 'cat',
						name: '有车',
						pic: '../../static/images/yc.jpg',
						checked:false
					},
				],
				current: -1,
				actionSheetList: ['汉', '畲'],
				actionSheetList1: ['博士', '硕士', '本科', '大专'],
				show: false,
				xuelishow: false,
				juzhudishow: false,
				avatar: '',
				cont:''
			}
		},
		onLoad() {
			let list = uni.getStorageSync('list')
			let room = uni.getStorageSync('room')
			let cat = uni.getStorageSync('cat')
			if(list.avatar == ''){
				this.avatar = uni.getStorageSync('avatar_url');
			}else{
				this.avatar = list.avatar;
				this.form.mingzu = list.mingzu;
				this.form.xueli = list.xueli;
				this.form.shengao = list.shengao;
				this.form.tizhong = list.tizhong;
				this.form.juzhudi = list.juzhudi;
				this.form.shouru = list.shouru;
				this.form.zhiye = list.zhiye;
				this.value = list.value;
				this.avatar = list.avatar
			}
			if(room.checked){
				this.items[0].checked = true
			}else{
				this.items[0].checked = false
			}
			if(cat.checked){
				this.items[1].checked = true
			}else{
				this.items[1].checked = false
			}
		},
		created() {
			// 监听从裁剪页发布的事件，获得裁剪结果
			uni.$on('uAvatarCropper', path => {
				this.avatar = path;
				// 可以在此上传到服务端
				// uni.uploadFile({
				// 	url: 'http://www.example.com/upload',
				// 	filePath: path,
				// 	name: 'file',
				// 	complete: (res) => {
				// 		console.log(res);
				// 	}
				// });
			})
		},
		methods: {
			// radioChange: function(evt) {
			// 	for (let i = 0; i < this.items.length; i++) {
			// 		if (this.items[i].value === evt.target.value) {
			// 			this.current = i;
			// 			uni.setStorageSync('radio',this.items[i])
			// 			break;
			// 		}
			// 	}
			// },
			checkboxChange(item,e) {
				this.cont = e.currentTarget.dataset.id
			    console.log(item.checked = !item.checked)
				if(this.cont == item.id){
					if(item.id == 1){
						let room = this.items[0]
						uni.setStorageSync('room',room)
					}else if(item.id == 2){
						let cat = this.items[1]
						uni.setStorageSync('cat',cat)
					}
				}
				if(item.id == 1 && item.checked == false){
					uni.removeStorageSync('room')
				}else if(item.id == 2 && item.checked == false){
					uni.removeStorageSync('cat')
				}
				
			},
			actionSheetCallback(index) {
				this.form.mingzu = this.actionSheetList[index];
			},
			actionSheetCallback1(index) {
				this.form.xueli = this.actionSheetList1[index];
			},
			actionSheetCallback2(index) {
				console.log(index)
				let area = index.area.label;
				let city = index.city.label;
				let province = index.province.label;
				this.form.juzhudi = province + city + area;
			},
			chooseAvatar() {
				// 此为uView的跳转方法，详见"文档-JS"部分，也可以用uni的uni.navigateTo
				this.$u.route({
					// 关于此路径，请见下方"注意事项"
					url: 'pages/u-avatar-cropper/u-avatar-cropper',
					// 内部已设置以下默认参数值，可不传这些参数
					params: {
						// 输出图片宽度，高等于宽，单位px
						destWidth: 300,
						// 裁剪框宽度，高等于宽，单位px
						rectWidth: 200,
						// 输出的图片类型，如果'png'类型发现裁剪的图片太大，改成"jpg"即可
						fileType: 'jpg',
					}
				})

			},
			submit(){
				this.$refs.uForm.validate(valid => {
					if (valid) {
						console.log('验证通过');
					} else {
						console.log('验证失败');
					}
				});
				this.$refs.uFor.validate(valid => {
					if (valid) {
						console.log('验证通过');
					} else {
						console.log('验证失败');
					}
				});
				
				uni.setStorage({
					key:'list',
					data:{
						mingzu:this.form.mingzu,
						xueli:this.form.xueli,
						shengao:this.form.shengao,
						tizhong:this.form.tizhong,
						juzhudi:this.form.juzhudi,
						shouru:this.form.shouru,
						zhiye:this.form.zhiye,
						value:this.value,
						avatar:this.avatar
					},
					success: (res) => {
						console.log(res)
						uni.showToast({
							title:'保存成功',
							icon:'none',
							duration:2000
						})
					}
				})
				
			}
			
		},
		onReady() {
				this.$refs.uForm.setRules(this.rules);
				this.$refs.uFor.setRules(this.rules);
			},
	}
</script>

<style lang="scss">
	page {
		padding-bottom: 150rpx;
		background-color: #F1F1F1;
	}


	// .wrap {
	// 	padding: 40rpx;
	// }

	// .u-avatar-wrap {
	// 	margin-top: 80rpx;
	// 	overflow: hidden;
	// 	margin-bottom: 80rpx;
	// 	text-align: center;
	// }

	// .u-avatar-demo {
	// 	width: 150rpx;
	// 	height: 150rpx;
	// 	border-radius: 100rpx;
	// }

	@import '/bjzl.scss';
</style>
