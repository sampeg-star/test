<template>
	<view>
	<u-navbar title="余额充值" title-color="white" back-icon-color="white" :background="background"></u-navbar>
	<view class="yecz_content">
		<view class="yecz_top">
		<view class="yecz_doll">
			{{meny}}元
		</view>
		<view class="yecz_text">
			当前余额
		</view>
		</view>
		<view class="yecz_choose">
			<view class="yecz_title">
				<text>请选择充值金额</text>
				<text style="color: #ff6e49;" @click="jump">余额明细</text>
			</view>
			<view class="yecz_box">
				<view class="yecz_ticker" v-for="(item,index) in list" :class="{active:cont == item.id}" :key="index" @click="change(item.meny,item,$event)" :data-id="item.id">
					<view class="yecz_nb">
						<view :class="{meny:cont != item.id}">{{item.meny}}</view>
						<text :class="{youhui:cont != item.id}">{{item.youhui}}</text>
					</view>
					
				</view>
			</view>
			<view class="yecz_btn" @click="chongzhi" :data-id="list">
						充值
			</view>
		</view>
	</view>
	</view>
</template>

<script>
	import cz from '../../data/data.js';
	export default{
		data(){
			return{
				background: {
					// 渐变色
					backgroundImage: 'linear-gradient(to right, rgb(255, 97, 51), rgb(255, 145, 70))'
					},
					list:[{
						id:1,
						meny:'10元',
						youhui:'优惠3元',
						flage:false
					},{
						id:2,
						meny:'20元',
						youhui:'优惠3元',
						flage:false
					},{
						id:3,
						meny:'30元',
						youhui:'优惠3元',
						flage:false
					},{
						id:4,
						meny:'40元',
						youhui:'优惠3元',
						flage:false
					},{
						id:5,
						meny:'50元',
						youhui:'优惠3元',
						flage:false
					},{
						id:6,
						meny:'60元',
						youhui:'优惠3元',
						flage:false
					},{
						id:7,
						meny:'70元',
						youhui:'优惠3元',
						flage:false
					},{
						id:8,
						meny:'80元',
						youhui:'优惠3元',
						flage:false
					},{
						id:9,
						meny:'90元',
						youhui:'优惠3元',
						flage:false
					}],
					cont:0,
					item:'',
					meny:500,
					list1:[],
					myjson:cz
			}
		},
		methods:{
			change(item,item1,e){
				this.cont = e.currentTarget.dataset.id;
				this.list1 = item1;
				console.log("list",this.list1)
				item = item.slice(0,-1)
				this.item = parseInt(item);
				console.log(this.item)
			},
			chongzhi(e){
				let formdata = [];
				let list = e.currentTarget.dataset.id;
				console.log("list",list)
				formdata.push(uni.getStorageSync('form'))
				for(let i = 0; i < formdata.length; i++){
					if(formdata[i] == ''){
						uni.navigateTo({
							url:'../zhuce/zhuce'
						})
					}else{
						// uni.setStorageSync('list1',this.list1);
						this.myjson.czmx.push(this.list1)
						uni.setStorageSync('item',this.item);
						if(this.cont > 0){
							this.meny = this.item + this.meny;
							uni.showToast({
							title:'充值成功',
							duration:2000,
							icon:'none'
							})
						}
						
					}
				}
			},
			jump(){
				// let onjs = JSON.stringify(uni.getStorageSync('list1'))
				uni.navigateTo({
					url:'../mx/yemx'
				})
			}
		}
	}
</script>

<style lang="scss">
	page{
		background-color: #F1F1F1;
	}
	.active{
		color: #FFFFFF;
		background-image:linear-gradient(to right,#ff6436, #ff8b4b) ;
	}
	@import '/yecz.scss';
</style>
