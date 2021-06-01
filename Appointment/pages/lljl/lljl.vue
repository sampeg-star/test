<template>
	<view class="lljl_content">
		<view v-if="lljljson.lljl1 != ''">
		<view class="lljl_nr" v-for="(item,index) in lljljson.lljl1" @click.stop="jump3(item,$event)" :key="item.id"
		:data-id="item.id">
			<image :src="item.pic" mode=""></image>
			<view class="lljl_text">
				<view class="lljl_name">
					{{item.name}}
				</view>
				<view class="lljl_msg">
					<image :src="item.pictag" mode=""></image>
					<text class="sex">{{item.tag[0]}}</text>
					<text>{{item.tag[1]}}</text>
				</view>
				<view class="lljl_tap">
					<text>{{item.jianjie}}</text>
					<view class="lljl_btn" v-if="item.flage" @click.stop="jump1(item,$event)" :data-click="item.id">关注</view>
					<view v-else class="lljl_btn" @click.stop="jump2(item,$event)" :data-click="item.id">
						已关注
					</view>
				</view>
			</view>
		</view>
		</view>
		<view v-else style="position: absolute; top: 50%; left: 50%; transform: translate(-50%,-50%);">
			暂无数据
		</view>
		<!-- <view class="lljl_nr">
			<image src="../../static/images/tx2.jpg" mode=""></image>
			<view class="lljl_text">
				<view class="lljl_name">
					王女士
				</view>
				<view class="lljl_msg">
					<image src="../../static/images/nv.jpg" mode=""></image>
					<text class="sex">女</text>
					<text>25岁</text>
				</view>
				<view class="lljl_tap">
					<text>想认识有钱的你</text>
					<view style="color: #ff4d2a;">
						已关注
					</view>
				</view>
			</view>
		</view>
		<view class="lljl_nr">
			<image src="../../static/images/tx3.jpg" mode=""></image>
			<view class="lljl_text">
				<view class="lljl_name">
					王先生
				</view>
				<view class="lljl_msg">
					<image src="../../static/images/nan.jpg" mode=""></image>
					<text class="sex" style="color: #96c9fe;">男</text>
					<text>25岁</text>
				</view>
				<view class="lljl_tap">
					<text>想认识有钱的你</text>
					<view style="color: #96c9fe;">
						已关注
					</view>
				</view>
			</view>
		</view>
		<view class="lljl_nr">
			<image src="../../static/images/tx2.jpg" mode=""></image>
			<view class="lljl_text">
				<view class="lljl_name">
					王女士
				</view>
				<view class="lljl_msg">
					<image src="../../static/images/nv.jpg" mode=""></image>
					<text class="sex">女</text>
					<text>25岁</text>
				</view>
				<view class="lljl_tap">
					<text>想认识有钱的你</text>
					<view class="lljl_btn">关注</view>
				</view>
			</view>
		</view> -->
	</view>
</template>

<script>
	import lljl from '../../data/data.js';
	export default{
		data(){
			return{
				// flage:true,
				flages:'',
				nickname:'',
				lljljson:lljl,
				look:'',
				cont:0,
				cont1:0,
				cont2:0
			}
		},
		onLoad() {
			this.look = uni.getStorageSync('look');
			var flage1 = uni.getStorageSync('flage');
			console.log("flage1",flage1)
			if(flage1 == -1){
				this.flage = false
				console.log('true')
			};
			for(let i = 0; i < this.lljljson.lljl1.length; i++){
				for(let j = i + 1; j < this.lljljson.lljl1.length; j++){
					if(this.lljljson.lljl1[i] == this.lljljson.lljl1[j]){
						j--;
						this.lljljson.lljl1.splice(j,1)
					}
				}
			}
		},
		methods:{
			jump1(item,e){
				var that = this;
				var formdata = [];
				that.nickname = uni.getStorageSync('nickname');
				formdata.push(uni.getStorageSync('form'));
				console.log(formdata)
				that.cont = e.currentTarget.dataset.click;
				if(item.id == that.cont){
					item.flage = false;
					that.lljljson.wdgz1.push(item)
					uni.showToast({
						title:'已关注',
						icon:'none',
						duration:2000
					})
				}
				if(that.nickname == ''){
					uni.navigateTo({
					url:'../login/login'	
					})
					
				}else{
					for(let i = 0; i < formdata.length; i++){
						if(formdata[i] == ''){
							uni.navigateTo({
							url:'../zhuce/zhuce'
							})
						}else{
							that.flages = -1;
							// that.flage = false;
							uni.setStorageSync('flage',that.flages)
						}
					}
				}
			},
			jump2(item,e){
				var that = this;
				// that.cont1 = e.currentTarget.dataset.click
				item.flage = true;
				// if(that.cont1 == item.id){
					// console.log(item)
					that.lljljson.wdgz1.splice(that.lljljson.wdgz1.indexOf(item),1)
				// }
				uni.showToast({
					title:'取消关注',
					duration:2000,
					icon:'none'
				})
			},
			jump3(item,e){
				var that =this;
				that.cont2 = e.currentTarget.dataset.click;
					let onjs = JSON.stringify(item)
					uni.navigateTo({
						url:'../dxxq/dxxq?add=' + onjs
					})
			}
		}
	}
</script>

<style lang="scss">
	page{
		background-color: #F1F1F1;
		padding-bottom: 50rpx;
	}
	@import '/lljl.scss';
</style>
