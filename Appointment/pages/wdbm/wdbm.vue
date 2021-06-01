<template>
	<view class="wdbm_content">
		<view v-if="bm">
		<view class="wdbm_nr" v-for="(item,index) in bmjson.wdbm" :key='item.id'>
			<image :src="item.pic" mode=""></image>
			<view class="wdbm_msg">
				<view class="wdbm_msg_title">
					{{item.title}}
				</view>
				<view class="wdbm_time">
					<text>{{item.begintime}}</text>
					<text>{{item.endtime}}</text>
				</view>
				<view class="wdbm_status">
					<text>报名人数：{{item.people_num}}人</text>
					<text>已报名</text>
				</view>
			</view>
		</view>
		</view>
		<view v-else style="position: absolute; left: 50%; top: 50%;
		transform: translate(-50%,-50%);">
			暂无数据
		</view>
		<!-- <view class="wdbm_nr">
			<image src="../../static/images/wdbm1.jpg" mode=""></image>
			<view class="wdbm_msg">
				<view class="wdbm_msg_title">
					只为寻找你
				</view>
				<view class="wdbm_time">
					<text>2021-03-25</text>
					<text>2021-03-25</text>
				</view>
				<view class="wdbm_status">
					<text>报名人数：65人</text>
					<text>已报名</text>
				</view>
			</view>
		</view>
		<view class="wdbm_nr">
			<image src="../../static/images/wdbm1.jpg" mode=""></image>
			<view class="wdbm_msg">
				<view class="wdbm_msg_title">
					只为寻找你
				</view>
				<view class="wdbm_time">
					<text>2021-03-25</text>
					<text>2021-03-25</text>
				</view>
				<view class="wdbm_status">
					<text>报名人数：65人</text>
					<text>已报名</text>
				</view>
			</view>
		</view>
		<view class="wdbm_nr">
			<image src="../../static/images/wdbm1.jpg" mode=""></image>
			<view class="wdbm_msg">
				<view class="wdbm_msg_title">
					只为寻找你
				</view>
				<view class="wdbm_time">
					<text>2021-03-25</text>
					<text>2021-03-25</text>
				</view>
				<view class="wdbm_status">
					<text>报名人数：65人</text>
					<text>已报名</text>
				</view>
			</view>
		</view> -->
	</view>
</template>

<script>
	import bm from '../../data/data.js';
	export default{
		data(){
			return{
				bmjson:bm,
				bm:''
			}
		},
		onLoad() {
			this.bm = uni.getStorageSync('bm')
		},
		methods:{
			
		}
	}
</script>

<style lang="scss">
	page{
		padding-bottom: 50rpx;
		background-color: #F1F1F1;
	}
	@import '/wdbm.scss';
</style>
