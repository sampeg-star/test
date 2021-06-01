<template>
	<view class="content">
		<u-navbar title="首页" :is-back="false" :background="background" title-color="white"></u-navbar>
		<view class="top_background">
		<view class="swiper_box">
			<u-swiper :list="list" mode="none" height="300"></u-swiper>
		</view>
		</view>
		<view class="index_nav">
			<view class="nav_men" @click="jump1()">
				<image src="../../static/images/zns.jpg" mode=""></image>
				<text>找男生</text>
			</view>
			<view class="nav_women" @click="jump1()">
				<image src="../../static/images/znr.jpg" mode=""></image>
				<text>找女生</text>
			</view>
			<view class="nav_city" @click="jump">
				<image src="../../static/images/tchd.jpg" mode=""></image>
				<text>同城活动</text>
			</view>
			<view class="nav_news" @click="jump2">
				<image src="../../static/images/xwdt.jpg" mode=""></image>
				<text>新闻动态</text>
			</view>
		</view>
		<view class="swiper_ad">
			<u-tag text="通知" type="warning" mode="plain"/>
			<view class="swiper_tz">
				<u-notice-bar mode="vertical" :list="listad" padding="0" :volume-icon="false" color="#c3c3c3" font-size="25"></u-notice-bar>
			</view>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="index_tj">
			<view class="index_tj_title">
				<view class="index_tj_title_text">
					<text></text>
					<view class="index_tj_text">
						对象推荐
					</view>
				</view>
				<view class="index_tj_more" @click="jump1">
					<view class="index_tj_more_title">
						更多
					</view>
					<u-icon name="arrow-right"></u-icon>
				</view>
			</view>
			<view class="index_list" v-for="(item,index) in myjson.data1" :key="item.id" @click="jump3(item,$event)" :data-add="item" :data-click="item.id">
				<view class="index_list_img">
					<image :src="item.pic" mode=""></image>
				</view>
				<view class="index_list_name">
					<view class="list_name">
						<view>{{item.name}}</view>
						<view><text class="cic"></text>两年内结婚</view>
					</view>
					<view class="index_list_tag">
						<view>{{item.tag.join(' | ')}}</view>
					</view>
					<view class="list_tag">
						<u-tag text="狮子座" type="error" mode="plain" size="mini"/>
						<u-tag text="单身" type="error" mode="plain" size="mini"/>
					</view>
					<view class="list_btn">
						<view v-if="item.flage" @click.stop="jump4(item,$event)" :data-click="item.id">关注</view>
						<view v-else @click.stop="jump5(item,index,$event)" :data-click="item.id">
							已关注
						</view>
					</view>
				</view>
			</view>
			<!-- <view class="index_list" @click="jump3">
				<view class="index_list_img">
					<image src="../../static/images/tx.jpg" mode=""></image>
				</view>
				<view class="index_list_name">
					<view class="list_name">
						<view>王女士</view>
						<view><text class="cic"></text>两年内结婚</view>
					</view>
					<view class="index_list_tag">
						<view>25岁</view>
						<text>|</text>
						<view>本科</view>
						<text>|</text>
						<view>176cm</view>
						<text>|</text>
						<view>5k-10k</view>
					</view>
					<view class="list_tag">
						<u-tag text="狮子座" type="error" mode="plain" size="mini"/>
						<u-tag text="单身" type="error" mode="plain" size="mini"/>
					</view>
					<view class="list_btn">
						<view v-if="flage" @click.stop="jump4(item.id,$event)" :data-click="item.id">关注</view>
						<view v-else @click.stop="jump5">
							已关注
						</view>
					</view>
				</view>
			</view>
			<view class="index_list" @click="jump3">
				<view class="index_list_img">
					<image src="../../static/images/tx.jpg" mode=""></image>
				</view>
				<view class="index_list_name">
					<view class="list_name">
						<view>王女士</view>
						<view><text class="cic"></text>两年内结婚</view>
					</view>
					<view class="index_list_tag">
						<view>25岁</view>
						<text>|</text>
						<view>本科</view>
						<text>|</text>
						<view>176cm</view>
						<text>|</text>
						<view>5k-10k</view>
					</view>
					<view class="list_tag">
						<u-tag text="狮子座" type="error" mode="plain" size="mini"/>
						<u-tag text="单身" type="error" mode="plain" size="mini"/>
					</view>
					<view class="list_btn">
						<view v-if="flage" @click.stop="jump4(item.id,$event)" :data-click="item.id">关注</view>
						<view v-else @click.stop="jump5">
							已关注
						</view>
					</view>
				</view>
			</view> -->
		</view>
	</view>
</template>

<script>
	import data2 from '../../data/data.js';
	export default {
		data() {
			return {
				list:[
					{
							image: 'https://cdn.uviewui.com/uview/swiper/1.jpg',
						},
						{
							image: 'https://cdn.uviewui.com/uview/swiper/2.jpg',
						},
						{
							image: 'https://cdn.uviewui.com/uview/swiper/3.jpg',
						}
				],
				background:{
					backgroundImage: 'linear-gradient(to right, rgb(255, 81, 46), rgb(255, 103, 53),rgb(255,132,64))'
				},
				listad: [
							'【重要提醒】请勿在个人介绍中留邮箱qq等联系方式，谨防上当受骗。',
							'通知通知',
					],
					// flage:true,
					flages:'',
					nickname:'',
					myjson:data2,
					is_login:false,
					cont:0,
					cont1:0,
					
			}
		},
		onLoad() {
			var flage1 = uni.getStorageSync('flage');
			console.log("flage1",flage1)
			if(flage1 == -1){
				this.flage = false
				console.log('true')
			};
			console.log('json',this.myjson)
			this.nickname = uni.getStorageSync('nickname');
			if(this.nickname == ""){
				uni.navigateTo({
					url:'../login/login'
				})
			}
		},
		methods: {
			jump(){
				var that = this;
				that.nickname = uni.getStorageSync('nickname');
				if(that.nickname != ''){
					uni.navigateTo({
					url:'../tc/tchd'
					})
				}else{
					uni.navigateTo({
						url:'../login/login'
					})
				}
				
			},
			jump1(){
				uni.switchTab({
					url:'../target/target'
				})
			},
			jump2(){
				var that = this;
				that.nickname = uni.getStorageSync('nickname');
				if(that.nickname != ''){
					uni.navigateTo({
					url:'../xwdt/xwdt'
					})
				}else{
					uni.navigateTo({
						url:'../login/login'
					})
				}
				
			},
			jump3(item,e){
				var that = this;
				let look = 1;
				var onjs;
				// if(!item.flage){
				// 	that.myjson.data1.flage = false
				// }
				uni.setStorageSync('look',look);
				that.nickname = uni.getStorageSync('nickname');
				if(that.nickname != ''){
					onjs = JSON.stringify(item)
					uni.navigateTo({
					url:'../dxxq/dxxq?add=' + onjs
					})
				}else{
					uni.navigateTo({
						url:'../login/login'
					})
				}
				// console.log('item',item)
				that.myjson.lljl1.push(item)
				console.log('1111',that.myjson.lljl1)
			},
			jump4(item,e){
				var that = this;
				that.cont = e.currentTarget.dataset.click;
				console.log(that.cont)
				if(that.cont == item.id){
					// console.log(item)
					item.flage = false;
					that.myjson.wdgz1.push(item)
					uni.showToast({
						title:'已关注',
						duration:2000,
						icon:'none'
					})
				}
				
				// var formdata = [];
				// that.nickname = uni.getStorageSync('nickname');
				// formdata.push(uni.getStorageSync('form'));
				// console.log(formdata)
				// if(that.nickname == ''){
				// 	uni.navigateTo({
				// 	url:'../login/login'	
				// 	})
					
				// }else{
				// 	for(let i = 0; i < formdata.length; i++){
				// 		if(formdata[i] == ''){
				// 			uni.navigateTo({
				// 			url:'../zhuce/zhuce'
				// 			})
				// 		}else{
							
				// 			that.flages = -1;//这个是存储的值
				// 			// that.flage = false;//这个是按钮切换
				// 			uni.setStorageSync('flage',that.flages)
				// 		}
				// 	}
				// }
				
				
			},
			jump5(item,index,e){
				var that = this;
				// that.cont1 = item.id;
				// console.log(that.cont1)
				// if(that.cont1 == item.id){
					// console.log(item)
					that.myjson.wdgz1.splice(that.myjson.wdgz1.indexOf(item),1)
				// }
				item.flage = true;
				uni.showToast({
					title:'取消关注',
					duration:2000,
					icon:'none'
				})
				uni.removeStorageSync('flage')
			}
		}
	}
</script>
<style lang="scss">
	page{
		background-color: #F1F1F1;
	}
@import '/index.scss';
</style>
