<template>
	<view class="tchd_content">
		<view class="top_box">
			<view class="tchd_banner">
			<image src="../../static/images/banner1.jpg" mode=""></image>
		</view>
		<view class="tchd_msg">
			<view class="tchd_title">
				相亲交友茫茫人海，只为寻找你
			</view>
			<view class="tchd_fx">
				<button type="default" open-type="share"><text>分享</text><image src="../../static/images/fx.jpg" mode=""></image></button>
			</view>
		</view>
		<view class="tchd_doll">
			<text class="tchd_meny">￥2500.00</text>
			<text class="tchd_people">300人已报名</text>
		</view>
		<view class="tchd_time">
			<view class="tchd_ks">
				<text>2021-03-25</text>
				<text class="ks_text">活动开始时间</text>
			</view>
			<text class="fg"></text>
			<view class="tchd_jz">
				<text>2021-03-25</text>
				<text class="jz_text">报名截止时间</text>
			</view>
		</view>
		</view>
		<view class="tchd_hdxq">
			<view class="tchd_hdxq_title">
				活动详情
			</view>
			<image src="../../static/images/hdtp.jpg" mode=""></image>
		</view>
		<view class="tchd_zx">
			<view class="zx_box">
				<view class="tchd_kf" @click="call()">
				<image src="../../static/images/dhkf2.jpg" mode=""></image>
				<text>咨询客服</text>
			</view>
			<view class="tchd_rx">
				<button type="default" open-type="contact">
				<image src="../../static/images/wxkf2.jpg" mode=""></image>
				<text>幸福热线</text>
				</button>
			</view>
			</view>
			<view v-if="list.bm == 1">
			<view class="tchd_bm" @click="jump" v-if="bm != 1 && !bm1">
				报名
			</view>
			<view class="tchd_bm" v-else @click="jump1">
				已报名
			</view>
			</view>
			<view v-else>
				<view class="tchd_bm">
					{{staust[list.bm]}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				bm1:'',
				bm:'',
				form:[],
				staust:[
					'未开始',
					'报名中',
					'已截止'
				],
				list:[]
			}
		},
		onLoad(op) {
			this.bm1 = uni.getStorageSync('bm')
			this.form.push(uni.getStorageSync('form'))
			this.list = JSON.parse(op.item)
			console.log(this.list)
		},
		methods:{
			jump(){
				for(let i = 0; i < this.form.length; i++){
					if(this.form[i] == ''){
						uni.navigateTo({
							url:'../zhuce/zhuce'
						})
					}else{
						uni.navigateTo({
							url:'../wdbm/wdbm'
						})
						this.bm = 1;
						uni.setStorageSync('bm',this.bm)
						uni.showToast({
							title:'报名成功',
							icon:'none',
							duration:2000
						})
					}
				}
				
				// uni.navigateTo({
				// 	url:'../wdbm/wdbm'
				// })
			},
			call(){
				uni.makePhoneCall({
					phoneNumber:'114'
				})
			},
			jump1(){
				uni.navigateTo({
					url:'../wdbm/wdbm'
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
	@import '/tchdxq.scss';
</style>
