<template>
	<view class="hyzx_content">
		<view class="hyzx_nr">
			<view class="hyzx_tick">
				<view class="hyzx_tick_ch" :class="{active:cont == item.id}" v-for="(item,index) in list" :key="index" @click="change" :data-id="item.id">
					<view class="hyzx_tick_title">
						{{item.title}}
					</view>
					<view class="hyzx_tick_fee">
						{{item.fee}}
					</view>
					<view class="hyzx_tick_month">
						{{item.month}}
					</view>
				</view>
				<!-- <view class="hyzx_tick_ch">
					<view class="hyzx_tick_title">
						xx年卡
					</view>
					<view class="hyzx_tick_fee">
						￥10
					</view>
					<view class="hyzx_tick_month">
						￥1元/12月
					</view>
				</view> -->
			</view>
			<view class="hyzx_btn">
				购买
			</view>
			<view class="hyzx_msg_title">
				<image src="../../static/images/ybr.jpg" mode=""></image>
				<text>当前会员特权</text>
				<image src="../../static/images/ybl.jpg" mode=""></image>
			</view>
			<view class="hyzx_tq">
				<view class="hyzx_tq_fi">
					<image src="../../static/images/ckxx.jpg" mode=""></image>
					<view class="hyzx_tq_fi_msg">
						查看详情信息
					</view>
					<view class="hyzx_tq_fi_cont">
						免费查看会员详情信息
					</view>
					
				</view>
				<view class="hyzx_tq_se">
					<image src="../../static/images/sfbz.jpg" mode=""></image>
					<view class="hyzx_tq_se_msg">
						会员身份标识
					</view>
					<view class="hyzx_tq_se_cont">
							身份加<image src="../../static/images/sfbz.jpg" mode=""></image>标识
					</view>
					<view style="color: rgb(173, 173, 173);">
						吸引更多关注
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				list:[
					{
						id:"1",
						title:"vip月卡",
						fee:"￥10",
						month:"￥10元/月"
					},
					{
						id:"2",
						title:"vip年卡",
						fee:"￥100",
						month:"￥100元/12月"
					}
				],
				cont:0
			}
		},
		methods:{
			change(e){
				this.cont = e.currentTarget.dataset.id;
				
			}
		}
	}
</script>

<style lang="scss">
	page{
		background-color: rgb(246, 246, 246);
	}
	.active{
		color: #FFFFFF;
		// background-image:linear-gradient(to right,#ff6436, #ff8b4b) ;
		background-color: #ff8b4b !important;
		// .hyzx_tick_fee{
		// 	color: #FFFFFF !important;
		// }
	}
	@import '/hyzx.scss';
</style>
