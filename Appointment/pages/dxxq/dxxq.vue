<template>
	<view class="dxxq_content">
		<view class="dxxq_top">
			<view class="dxxq_img">
				<image :src="list.pic" mode=""></image>
			</view>
			<view class="dxxq_msg">
				<view class="msg_name">
					{{list.name}}
				</view>
				<view class="msg_zl">
					<text>{{list.tag}}</text>
				</view>
				<view class="msg_tag">
					<view class="tag">
						<u-tag text="单身" mode="plain" type="error" size="mini"/>
						<u-tag text="射手座" mode="plain" type="error" size="mini" style="margin-left: 10rpx; margin-right: 10rpx;"/>
						<u-tag text="福州" mode="plain" type="error" size="mini"/>
					</view>
					<view class="msg_btn" v-if="list.flage" @click.stop="jump4(list,$event)" :data-click="list.id">关注</view>
					<view class="msg_btn" v-else @click.stop="jump5(list,$event)" :data-click="list.id">
						已关注
					</view>
				</view>
			</view>
		</view>
		<view class="dxxq_jbzl">
			<view class="dxxq_title">
				基本资料
			</view>
			<view class="dxxq_fi">
				<view class="dxxq_mz">
					<text>民族</text>
					<text>汉</text>
				</view>
				<view class="dxxq_xl">
					<text>学历</text>
					<text>本科</text>
				</view>
			</view>
			<view class="dxxq_se">
				<view class="dxxq_sn">
					<text>职业</text>
					<text>室内设计</text>
				</view>
				<view class="dxxq_nsr">
					<text>年收入</text>
					<text>20w-30w</text>
				</view>
			</view>
			<view class="dxxq_tr">
				<view class="dxxq_tz">
					<text>体重</text>
					<text>50kg</text>
				</view>
				<view class="dxxq_zstj">
					<text>自身条件</text>
					<text>有车</text>
				</view>
			</view>
			<view class="dxxq_jzd">
				<text>居住地</text>
				<text>北京市市辖区东城区</text>
			</view>
		</view>
		<view class="dxxq_xc">
			<view class="xc_title">
				Ta的相册
			</view>
			<view class="xc_image">
				<scroll-view scroll-x="true" class="pic" style="width: 100%;overflow:hidden;white-space:nowrap;">
				<view class="img_wrapper"  v-for="(item,index) in images" :key="index">
				<image @click="imageclick(images)" :src="item" mode="" style="width: 100%;height: 100%;"></image></view>
				</scroll-view>
			</view>
		</view>
		<view class="dxxq_zwjs">
			<view class="zwjs_title">
				自我介绍
			</view>
			<view class="zwjs_nr">
				　　我的性格活泼开朗，爱说爱笑，喜欢跟人开玩笑，我幼稚调皮，异想天开，是个十分乐观的女孩子。
			</view>
		</view>
		<view class="dxxq_btn_box">
			<view class="dxxq_btn" @click="call()">
			联系Ta
			</view>
		</view>
		
	</view>
</template>

<script>
	import myjson from '../../data/data.js';
	export default{
		data(){
			return{
				images:['../../static/logo.png','../../static/images/tx.jpg','../../static/images/tx.jpg','../../static/images/tx.jpg','../../static/images/tx.jpg'],
				flage:true,
				flages:'',
				list:[],
				cont:0,
				cont1:0,
				myjson:myjson
			}
		},
		onLoad(op) {
			var flage1 = uni.getStorageSync('flage');
			console.log("flage1",flage1)
			if(flage1 == -1){
				this.flage = false
				console.log('true')
			};
			this.list = JSON.parse(op.add)
			console.log(this.list)
			 
		},
		methods:{
			imageclick(file){
				uni.previewImage({
					urls:file,
				})
			},
			call(){
				uni.makePhoneCall({
					phoneNumber:'114'
				})
			},
			jump4(item,e){
				var that = this;
				that.cont = e.currentTarget.dataset.click;
				// console.log(this.cont)
					// console.log(item)
				that.list.flage = false;
				uni.showToast({
					title:'已关注',
					icon:'none',
					duration:2000
				})
				that.myjson.wdgz1.push(item)
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
							
							that.flages = -1;//这个是存储的值
							// that.flage = false;//这个是按钮切换
							uni.setStorageSync('flage',that.flages)
						}
					}
				}
				
				
			},
			jump5(item,e){
				var that = this;
				// that.cont1 = e.currentTarget.dataset.click;
				// console.log(that.cont1)
				
				// if(that.cont1 == item.id){
					// console.log(item)
					that.myjson.wdgz1.splice(that.myjson.wdgz1.indexOf(item),1)
				// }
				that.list.flage = true;
				
				uni.removeStorageSync('flage')
				uni.showToast({
					title:'取消关注',
					icon:'none',
					duration:2000
				})
			}
		}
	}
</script>

<style lang="scss">
	page{
		padding-bottom: 150rpx;
		background-color: #F1F1F1;
	}
	@import '/dxxq.scss';
</style>
