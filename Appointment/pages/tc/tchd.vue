<template>
	<view class="tc_content">
		<view class="tc_nr" @click="jump(item,$event)" v-for="(item,index) in tchdjson.tchd" :key="item.id"
		:data-status="item.staust" :data-id="item.id">
			<image :src="item.pic" mode=""></image>
			<view class="tc_text">
				<view class="tc_title">
					<view class="tc_fi_title">
						{{item.title}}
					</view>
					<view class="tc_se_title">
						{{staust[item.bm]}}
					</view>
				</view>
				<view class="tc_ks_time">
					活动开始时间：{{item.begintime}}
				</view>
				<view class="tc_jz_time">
					报名截止时间：{{item.endtime}}
				</view>
			</view>
		</view>
		<!-- <view class="tc_nr" @click="jump">
			<image src="../../static/images/xqjy.jpg" mode=""></image>
			<view class="tc_text">
				<view class="tc_title">
					<view class="tc_fi_title">
						相亲交友
					</view>
					<view class="tc_se_title">
						报名中
					</view>
				</view>
				<view class="tc_ks_time">
					活动开始时间：2021-11-02
				</view>
				<view class="tc_jz_time">
					报名截止时间：2022-02-12
				</view>
			</view>
		</view>
		<view class="tc_nr" @click="jump">
			<image src="../../static/images/xqjy.jpg" mode=""></image>
			<view class="tc_text">
				<view class="tc_title">
					<view class="tc_fi_title">
						相亲交友
					</view>
					<view class="tc_se_title">
						报名中
					</view>
				</view>
				<view class="tc_ks_time">
					活动开始时间：2021-11-02
				</view>
				<view class="tc_jz_time">
					报名截止时间：2022-02-12
				</view>
			</view>
		</view>
		<view class="tc_nr" @click="jump">
			<image src="../../static/images/xqjy.jpg" mode=""></image>
			<view class="tc_text">
				<view class="tc_title">
					<view class="tc_fi_title">
						相亲交友
					</view>
					<view class="tc_se_title">
						报名中
					</view>
				</view>
				<view class="tc_ks_time">
					活动开始时间：2021-11-02
				</view>
				<view class="tc_jz_time">
					报名截止时间：2022-02-12
				</view>
			</view>
		</view>
		<view class="tc_nr">
			<image src="../../static/images/xqjy.jpg" mode=""></image>
			<view class="tc_text">
				<view class="tc_title">
					<view class="tc_fi_title">
						相亲交友
					</view>
					<view class="tc_se_title">
						报名中
					</view>
				</view>
				<view class="tc_ks_time">
					活动开始时间：2021-11-02
				</view>
				<view class="tc_jz_time">
					报名截止时间：2022-02-12
				</view>
			</view>
		</view> -->
	</view>
</template>

<script>
	import tchd from '../../data/data.js';
	export default{
		data(){
			return{
				tchdjson:tchd,
				staust:[
					'未开始',
					'报名中',
					'已截止'
				],
				cont:0
			}
		},
		methods:{
			jump(item,e){
				
				if(this.cont = e.currentTarget.dataset.id){
					let onjs = JSON.stringify(item)
					uni.navigateTo({
					url:'../tcgdxq/tchdxq?item=' + onjs
					})
				}
				
				
			}
		}
	}
</script>

<style lang="scss">
	page{
		background-color: #F1F1F1;
		padding-bottom: 50rpx;
	}
	@import '/tchd.scss';
</style>
