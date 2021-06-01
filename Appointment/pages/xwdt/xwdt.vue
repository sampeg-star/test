<template>
	<view class="xwdt_content">
		<view class="xwdt_title">
			<view class="xwdt_title_tap" v-for="(item,index) in listtab" :key="item.id" @click="change" :class="{dis:cont == item.id}" :data-id="item.id">
				{{item.name}}
				<text :class="{bor:cont == item.id}"></text>
			</view>
		</view>
			<view class="end" :class="{endshow:cont == 1}">
				<view class="xwdt_nr" @click="jump(item,$event)" v-for="(item,index) in xwdtjson.dontai1" :key="item.id" 
				:data-id="item.id">
					<image :src="item.pic" mode=""></image>
					<view class="xwdt_text">
						<view class="xwdt_text_title">
							{{item.title}}
						</view>
						<view class="xwdt_text_time">
							<text>{{item.num}}阅读</text>
							<text>{{item.updata}}</text>
						</view>
					</view>
				</view>
				<!-- <view class="xwdt_nr" @click="jump">
					<image src="../../static/images/xw.jpg" mode=""></image>
					<view class="xwdt_text">
						<view class="xwdt_text_title">
							标题标题标题标题标题标题标题标题标题标题
						</view>
						<view class="xwdt_text_time">
							<text>1584阅读</text>
							<text>2020-01-25</text>
						</view>
					</view>
				</view> -->
			</view>
			<view class="end" :class="{endshow:cont == 2}">
				<view class="xwdt_nr" @click="jump(item,$event)" v-for="(item,index) in xwdtjson.marry1" :key="item.id" :data-id="item.id">
					<image :src="item.pic" mode=""></image>
					<view class="xwdt_text">
						<view class="xwdt_text_title">
							{{item.title}}
						</view>
						<view class="xwdt_text_time">
							<text>{{item.num}}阅读</text>
							<text>{{item.updata}}</text>
						</view>
					</view>
				</view>
			</view>
			<view class="end" :class="{endshow:cont == 3}">
				<view class="xwdt_nr" @click="jump(item,$event)" v-for="(item,index) in xwdtjson.qingan1" :key="item.id" :data-id="item.id">
					<image :src="item.pic" mode=""></image>
					<view class="xwdt_text">
						<view class="xwdt_text_title">
							{{item.title}}
						</view>
						<view class="xwdt_text_time">
							<text>{{item.num}}阅读</text>
							<text>{{item.updata}}</text>
						</view>
					</view>
				</view>
				<!-- <view class="xwdt_nr">
					<image src="../../static/images/xw.jpg" mode=""></image>
					<view class="xwdt_text">
						<view class="xwdt_text_title">
							标题标题标题标题标题标题标题标题标题标题
						</view>
						<view class="xwdt_text_time">
							<text>1584阅读</text>
							<text>2020-01-25</text>
						</view>
					</view>
				</view> -->
			</view>
			<view class="end" :class="{endshow:cont == 4}">
				<view class="xwdt_nr" @click="jump(item,$event)" v-for="(item,index) in xwdtjson.hanye1" :key="item.id" :data-id="item.id">
					<image :src="item.pic" mode=""></image>
					<view class="xwdt_text">
						<view class="xwdt_text_title">
							{{item.title}}
						</view>
						<view class="xwdt_text_time">
							<text>{{item.num}}阅读</text>
							<text>{{item.updata}}</text>
						</view>
					</view>
				</view>
			</view>
	</view>
</template>

<script>
	import xwdt from '../../data/data.js';
	export default{
		data(){
			return{
				xwdtjson:xwdt,
				listtab:[
					{
						id:1,
						name:'新闻动态'
					},
					{
						id:2,
						name:'婚姻殿堂'
					},
					{
						id:3,
						name:'情感日记'
					},
					{
						id:4,
						name:'行业资讯'
					}
				],
				cont:1,
				cont1:0
			}
		},
		methods:{
			change(e){
				this.cont = e.currentTarget.dataset.id;
			},
			jump(item,e){
				this.cont1 = e.currentTarget.dataset.id;
				let onjs = JSON.stringify(item)
				if(this.cont1 == item.id){
					uni.navigateTo({
					url:'../wzxq/wzxq?id=' + onjs
					})
				}
				
			}
		}
	}
</script>

<style lang="scss">
	page{
		padding-bottom: 50rpx;
		background-color: #F1F1F1;
	}
	@import '/xwdt.scss';
</style>
