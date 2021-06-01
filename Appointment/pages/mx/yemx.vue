<template>
	<view class="mx_content">
		<view v-if="czmxjson.czmx != ''">
		<view class="mx_nr" v-for="(item,index) in czmxjson.czmx" :key="item.id">
			<view class="mx_fee">
				<text>充值</text>
				<text>+{{item.meny}}</text>
			</view>
			<view class="mx_time">
				<text>{{item.youhui}}</text>
				<text>{{time}}</text>
			</view>
		</view>
		</view>
		<view v-else style="position: absolute; top: 50%; left: 50%;
		transform: translate(-50%,-50%);">
			暂无数据
		</view>
		<!-- <view class="mx_nr">
			<view class="mx_fee">
				<text>充值</text>
				<text>-30元</text>
			</view>
			<view class="mx_time">
				<text>购买会员</text>
				<text>2021-12-26</text>
			</view>
		</view>
		<view class="mx_nr">
			<view class="mx_fee">
				<text>充值</text>
				<text>-30元</text>
			</view>
			<view class="mx_time">
				<text>购买会员</text>
				<text>2021-12-26</text>
			</view>
		</view>
		<view class="mx_nr">
			<view class="mx_fee">
				<text>充值</text>
				<text>-30元</text>
			</view>
			<view class="mx_time">
				<text>购买会员</text>
				<text>2021-12-26</text>
			</view>
		</view>
		<view class="mx_nr">
			<view class="mx_fee">
				<text>充值</text>
				<text>-30元</text>
			</view>
			<view class="mx_time">
				<text>购买会员</text>
				<text>2021-12-26</text>
			</view>
		</view> -->
	</view>
</template>

<script>
	import mx from '../../data/data.js';
	export default{
		data(){
			return{
				czmxjson:mx,
				item:'',
				time:''
			}
		},
		onLoad(op) {
			// let onjs = JSON.parse(op.add)
			this.item = uni.getStorageSync('item')
			// this.czmxjson.czmx.push(uni.getStorageSync('list1'));
			let d = new Date();
			let y = d.getFullYear();
			let m = d.getMonth() + 1;
			let day = d.getDate();
			this.time = y + "-" + m  + "-" + day
		},
		methods:{
			
		}
	}
</script>

<style lang="scss">
	page{
		background-color: #F1F1F1;
		padding-bottom: 50rpx;
	}
	@import '/yemx.scss';
</style>
