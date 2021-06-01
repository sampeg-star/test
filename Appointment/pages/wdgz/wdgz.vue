<template>
	<view class="lljl_content">
		<view v-if="wdgzjson.wdgz1 != ''">
		<view class="lljl_nr" v-for="(item,index) in wdgzjson.wdgz1" :key="item.id" @click="jump2(item,$event)"
		:data-id="item.id">
			<image :src="item.pic" mode=""></image>
			<view class="lljl_text">
				<view class="lljl_name">
					{{item.name}}
				</view>
				<view class="lljl_msg">
					<image :src="item.pictag" mode=""></image>
					<text class="sex">{{item.tag[0]}}</text>
					<text>{{item.tag.slice(1)}}</text>
				</view>
				<view class="lljl_tap">
					<text>{{item.jianjie}}</text>
					<view style="color: #ff4d2a;">
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
		</view> -->
		
	</view>
</template>

<script>
	import wdgz from '../../data/data.js';
	export default{
		data(){
			return{
				// flage:true,
				flages:'',
				nickname:'',
				flage1:'',
				wdgzjson:wdgz,
				look:'',
				cont:0
			}
		},
		onLoad() {
			this.look = uni.getStorageSync('look');
			this.flage1 = uni.getStorageSync('flage');
			console.log("flage1",this.flage1)
			if(this.flage1 == -1){
				this.flage = false
				console.log('true')
			};
			for(let i = 0; i < this.wdgzjson.wdgz1.length; i++){
				for(let j = i + 1; j < this.wdgzjson.wdgz1.length; j++){
					if(this.wdgzjson.wdgz1[i] == this.wdgzjson.wdgz1[j]){
						j--;
						this.wdgzjson.wdgz1.splice(j,1)
					}
				}
			}
		},
		methods:{
			jump1(){
				var that = this;
				var formdata = [];
				that.nickname = uni.getStorageSync('nickname');
				formdata.push(uni.getStorageSync('form'));
				console.log(formdata)
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
				let onjs = JSON.stringify(item);
				this.cont = e.currentTarget.dataset.id;
				if(this.cont == item.id){
					uni.navigateTo({
					url:'../dxxq/dxxq?add=' + onjs
				})
				}
				this.wdgzjson.lljl1.push(item)
			}
		}
	}
</script>

<style lang="scss">
	page{
		background-color: #F1F1F1;
		padding-bottom: 50rpx;
	}
	@import '/wdgz.scss';
</style>
