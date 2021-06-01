<template>
	<view class="zhuce_content">
		<view class="icon" @click.stop="back"><u-icon name="arrow-left"size="60" style="position: absolute; top: 110rpx;left: 30rpx;"></u-icon></view>
		
		<image src="../../static/images/topbanner.jpg" mode=""></image>
		<view style="padding-left: 30rpx;padding-right: 30rpx;">
			<u-form :model="form" ref="uForm">
				<u-form-item label-width="180" label="真实姓名:" prop="name"><u-input v-model="form.name" placeholder="请输入姓名" placeholder-style="color: #c0c4cc"/></u-form-item>
				<u-form-item label-width="180" label="联系电话:" prop="intro"><u-input v-model="form.intro" placeholder="请输入电话号码" placeholder-style="color: #c0c4cc"/></u-form-item>
				<u-form-item label-width="180" label="性别:" prop="sex">
					<!-- <u-input v-model="form.sex" :clearable='false' @click="show = true" type="select" placeholder-style="color:#ffffff"/> -->
					<view @click="show = true"  style="width: 100%;display: flex;justify-content: space-between;">
						<text>{{form.sex}}</text>
						<u-icon name="arrow-right" ></u-icon>
					</view>
				<!-- <u-icon name="arrow-right" style="display: inline-block;"></u-icon> -->
				</u-form-item>
				<u-form-item label-width="180" label="出生年月:" prop="born">
					<!-- <u-input v-model="form.born" :clearable='false' type="select"  @click="showtime = true" placeholder-style="color:#ffffff"/> -->
					<view @click="showtime = true" style="width: 100%;display: flex;justify-content: space-between;">
						<text>{{form.born}}</text>
						<u-icon name="arrow-right"></u-icon>
					</view>
				</u-form-item>
				<u-form-item label-width="180" label="身份证号码:" prop="sfid"><u-input v-model="form.sfid" placeholder-style="color: #c0c4cc"/></u-form-item>
			</u-form>
		</view>
		
			<u-select v-model="show" mode="single-column" :list="sexlist" @confirm="confirm"></u-select>
			<u-picker mode="time" v-model="showtime" @confirm="borntime"></u-picker>
			
			<view class="sub" @click="submit">提交</view>
			<view class="xieyi">
				<u-checkbox-group>
					<u-checkbox icon-size="30" size="40" v-model="checked" shape="circle" :data-check="'checked'">我已阅读并且了解
						  <text @click.stop="jump">[注册会员协议声明]</text></u-checkbox>
				</u-checkbox-group>
				<!-- <checkbox-group>
				      <label>
				          <checkbox value="cb" checked="true"/>我已阅读并且了解
						  <text>[注册会员协议声明]</text>
				      </label>
				</checkbox-group> -->
			</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				form: {
					name: '',
					intro: '',
					sex: '',
					born:'',
					sfid:''
				},
				rules: { //表单验证
								name: [
									{
										required: true,
										message: '请输入姓名',
										// 可以单个或者同时写两个触发验证方式
										trigger: 'change'
									}
								],
								sex: [
									{
										required: true,
										message: '请选择性别',
										trigger: 'change'
									}
								],
								intro:[
									{
										required: true,
										message: '请输入手机号',
										trigger: 'change'
									},
									{
												pattern: /^1[0-9]{10,10}$/,
												// 正则检验前先将值转为字符串
												transform(value) {
													return String(value);
												},
												message: '输入正确手机号码'
											},
								],
								sfid:[
									{
										required: true,
										message: '请输身份证号',
										trigger: 'change'
									},
									{
										pattern:/^[1-9]\d{5}[1-9]\d{3}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])\d{3}([0-9]|X)$/,
										transform(value) {
											return String(value);
										},
										message: '输入正确身份证号码'
									}
								],
								born:[
									{
										required: true,
										message: '请选择出生年月',
										trigger: 'change'
									}
								]
							},
				show:false,
				showtime:false,
				checked:false,
				sexlist:[
					{
						value: '1',
						label: '男'
					},
					{
						value: '2',
						label: '女'
					}
				],
			}
		},
		
		methods:{
			confirm(e){
				this.form.sex = e[0].label
			},
			submit() {
				var arr =[];
						this.$refs.uForm.validate(valid => {
							if (valid) {
								console.log('验证通过');
							} else {
								console.log('验证失败');
							}
						});
						for(let i in this.form){
							console.log(this.form[i])
							arr.push(this.form[i])
							console.log(arr)
						}
						for(var i = 0 ; i < arr.length; i++){
							if(arr.indexOf('') == -1 && this.checked == true){
									uni.setStorage({
										key:'form',
										data:{
											name: this.form.name,
											intro: this.form.intro,
											sex: this.form.sex,
											born:this.form.born,
											sfid:this.form.sfid	
											
										},
										success: (res) => {
											console.log(res)
											uni.showToast({
												title:'注册成功',
												duration:2000,
												icon:'none'
											});
											uni.reLaunch({
												url:'../index/index'
											})
										}
									})
							}else{
								if(arr.indexOf('') == -1 ){
									uni.showToast({
										title:'请勾选协议',
										icon:'none',
										duration:2000
									})
								}
							}
							
						}
					},
			borntime(index){
				let year = index.year;
				let month = index.month;
				let day = index.day;
				this.form.born = year + "-" + month + "-" + day;
				// console.log(index)
			},
			jump(e){
				uni.navigateTo({
					url:'../sm/sm'
				})
			},
			back(){
				uni.reLaunch({
					url:'../index/index'
				})
			}
		},
		onReady() {
				this.$refs.uForm.setRules(this.rules);
			},
	}
</script>

<style lang="scss">
	
	@import '/zhuce.scss';
</style>
