<template>
	<view class="content">
		<view class="target_nav">
			<view class="target_choose">
				已选
			</view>
			<scroll-view scroll-x="true" style="width: 60%;overflow:hidden;white-space:nowrap;">
				<view class="tap" v-for="(item,index) in list1" :key="index"><text class="choose">{{item.text}}</text><u-icon @click="close(item)" name="close" size="20" color="#ff4c2a"></u-icon></view>
				
			</scroll-view>
			<view class="target_choose_nr" @click="showpop">
				<text>筛选</text>
				<u-icon  name="arrow-down" color="#ff4c2a"></u-icon>
			</view>
		</view>
		<u-popup v-model="show" mode="top" z-index="1" height="1200" :mask="false" >
			<view style="padding-bottom: 200rpx;padding-top: 30rpx;">
					<view class="age" style="margin-top: 100rpx;">
						<view class="age_title">
							年龄
						</view>
						<view class="age_choose">
							<view v-for="(item,index) in list" :class="{'active':list1.indexOf(item) !=-1}"  :key="index" :data-id="item.id" @click="change(item)">
								{{item.text}}
							</view>
							
						</view>
					</view>
					<view class="sg" style="margin-top: 100rpx;">
						<view class="sg_title">
							身高
						</view>
						<view class="sg_choose">
							<view v-for="(item,index) in sglist" :class="{'active':list1.indexOf(item) !=-1}" :key="index" :data-id="item.id" @click="changesg(item)">
								{{item.text}}
							</view>
							
						</view>
					</view>
					<view class="xl" style="margin-top: 100rpx;">
						<view class="xl_title">
							学历
						</view>
						<view class="xl_choose">
							<view v-for="(item,index) in xllist" :class="{'active':list1.indexOf(item) !=-1}" :key="index" :data-id="item.id" @click="changexl(item)">
								{{item.text}}
							</view>
							
						</view>
					</view>
					<view class="target_choose_box">
						<view class="target_choose_btn" @click="fiflter">
							确定
						</view>
					</view>
					
					</view>
		</u-popup>
		<view v-if="list1 != ''">
		<view class="target_box" style="z-index: -3;" @click="jump(item,$event)" v-for="(item,index) in arrlist" :key="item.id"
		:data-click="item.id" :data-add="item">
			<view class="target_img">
				<image :src="item.pic" mode=""></image>
			</view>
			<view class="target_js">
				<view class="target_name">
					{{item.name}}
				</view>
				<view class="target_fi">
					<view class="target_se">
						<view class="target_tr">
							<view class="target_th">
							<image :src="item.pictag" mode=""></image>
								<text>{{item.tag[0]}}</text>
							</view>
							<text style="font-size: 22rpx;width: 208rpx;">{{item.tag.slice(1).join('')}}</text>
						</view>
						<view class="target_fif">
							{{item.jianjie}}
						</view>
					</view>
					<view class="target_btn">
						<view v-if="item.flage" @click.stop="jump1(item,$event)" :data-click="item.id">关注</view>
						<view v-else @click.stop="jump2(item)">
							已关注
						</view>
					</view>
				</view>
			</view>
		</view>
		</view>
		<view v-else>
		<view class="target_box" style="z-index: -3;" @click="jump(item,$event)" v-for="(item,index) in targetjson.data1" :key="item.id"
		:data-click="item.id" :data-add="item">
			<view class="target_img">
				<image :src="item.pic" mode=""></image>
			</view>
			<view class="target_js">
				<view class="target_name">
					{{item.name}}
				</view>
				<view class="target_fi">
					<view class="target_se">
						<view class="target_tr">
							<view class="target_th">
							<image :src="item.pictag" mode=""></image>
								<text>{{item.tag[0]}}</text>
							</view>
							<text style="font-size: 22rpx;width: 208rpx;">{{item.tag.slice(1).join(' | ')}}</text>
						</view>
						<view class="target_fif">
							{{item.jianjie}}
						</view>
					</view>
					<view class="target_btn">
						<view v-if="item.flage" @click.stop="jump1(item,$event)" :data-click="item.id">关注</view>
						<view v-else @click.stop="jump2(item,$event)" :data-click="item.id">
							已关注
						</view>
					</view>
				</view>
			</view>
		</view>
		</view>
		<!-- <view class="target_box" style="z-index: -3;" @click="jump">
			<view class="target_img">
				<image src="../../static/images/tx2.jpg" mode=""></image>
			</view>
			<view class="target_js">
				<view class="target_name">
					柠檬小可爱
				</view>
				<view class="target_fi">
					<view class="target_se">
						<view class="target_tr">
							<view class="target_th">
							<image src="../../static/images/nv.jpg" mode=""></image>
								<text>女</text>
							</view>
							<text>26岁</text>
						</view>
						<view class="target_fif">
							想认识有钱的你
						</view>
					</view>
					<view class="target_btn">
						<view>关注</view>
					</view>
				</view>
			</view>
		</view>
		<view class="target_box" style="z-index: -3;" @click="jump">
			<view class="target_img">
				<image src="../../static/images/tx2.jpg" mode=""></image>
			</view>
			<view class="target_js">
				<view class="target_name">
					柠檬小可爱
				</view>
				<view class="target_fi">
					<view class="target_se">
						<view class="target_tr">
							<view class="target_th">
							<image src="../../static/images/nv.jpg" mode=""></image>
								<text>女</text>
							</view>
							<text>26岁</text>
						</view>
						<view class="target_fif">
							想认识有钱的你
						</view>
					</view>
					<view class="target_btn">
						关注
					</view>
				</view>
			</view>
		</view> -->
	</view>
</template>

<script>
	import target from "../../data/data.js";
	export default {
		data() {
			return {
				list:[{id:1,text:'不限'},{id:2,text:'18-20岁'},{id:3,text:'20-25岁'},
				{id:4,text:'25-30岁'},{id:5,text:'30-35岁'},{id:6,text:'35-40岁'},
				{id:7,text:'40-45岁'},{id:8,text:'45-50岁'},{id:9,text:'50-55岁'},
				],
				sglist:[
					{id:1,text:'不限'},{id:2,text:'156-160cm'},{id:3,text:'160-165cm'},
					{id:4,text:'165-170cm'},{id:5,text:'170-175cm'},{id:6,text:'175-180cm'},
					{id:7,text:'180-185cm'},{id:8,text:'185-190cm'},
				],
				xllist:[
					{id:1,text:'不限'},{id:2,text:'初中以下'},{id:3,text:'中专/高中'},
					{id:4,text:'大专'},{id:5,text:'本科'},{id:6,text:'硕士'},
					{id:7,text:'博士'},
				],
				show:false,
				list1:[],//总的数组
				nllist:[],//年龄的新数组
				sglist1:[],//身高的新数组
				xllist1:[],//学历的新数组
				choose:false,
				cont:"",
				// flage:true,
				flages:'',
				nickname:'',
				targetjson:target,
				arrlist:[],
				cont1:0,
				result:[]
				
			}
		},
		onLoad() {
			var flage1 = uni.getStorageSync('flage');
			console.log("flage1",flage1)
			if(flage1 == -1){
				this.flage = false
				console.log('true')
			};
			this.nickname = uni.getStorageSync('nickname');
			if(this.nickname == ""){
				uni.navigateTo({
					url:'../login/login'
				})
			}
		},
		methods: {
			showpop(){
				this.show = !this.show;
			},
			change(e){
				var arr;
					if(this.nllist.indexOf(e) == -1){
						if(e.id != 1){
							this.nllist.push(e);//当点击数组除“不限”外的添加数组
							for(let i =0; i < this.nllist.length; i++){
								if(this.nllist[i].id == 1){
									this.nllist.splice(0,1);//如果点击时数组的id为1就是“不限”删除这个数组选项
									this.list1 = this.nllist.concat(this.sglist1,this.xllist1);
									//总筛选栏呈现的数组合并三个数组
								}else{
									this.list1 = this.nllist.concat(this.sglist1,this.xllist1);
								}
							}
							// this.list1 = this.nllist.concat(this.sglist1,this.xllist1);
							console.log(this.nllist)
						}else{
							this.nllist.push(e);
							arr = this.nllist.slice(-1);//截取数组最后一个元素
							this.nllist = arr;//再赋值给数组
							console.log('1',arr)
							this.list1 = this.xllist1.concat(this.sglist1,this.nllist);//这里再次合并数组
						}
					}else{
					this.nllist.splice(this.nllist.indexOf(e),1);//再次点击删除元素
					this.list1 = this.nllist.concat(this.sglist1,this.xllist1);
					}
					console.log(this.list1)
			},
			changesg(e){
				var sgarr;
					if(this.sglist1.indexOf(e) == -1){
						if(e.id != 1){
							this.sglist1.push(e);
							for(let i =0; i < this.sglist1.length; i++){
								if(this.sglist1[i].id == 1){
									this.sglist1.splice(0,1);
									this.list1 = this.nllist.concat(this.sglist1,this.xllist1);
								}else{
									this.list1 = this.nllist.concat(this.sglist1,this.xllist1);
								}
							}
						}else{
							this.sglist1.push(e);
							sgarr = this.sglist1.slice(-1)
							this.sglist1 = sgarr;
							this.list1 = this.xllist1.concat(this.sglist1,this.nllist);
						}
					}else{
					this.sglist1.splice(this.sglist1.indexOf(e),1);
					this.list1 = this.nllist.concat(this.sglist1,this.xllist1);
					}
			console.log(this.list1)
			},
			changexl(e){
				var xlarr;
					if(this.xllist1.indexOf(e) == -1){
						if(e.id != 1){
							this.xllist1.push(e);
							for(let i = 0; i < this.xllist1.length; i++){
								if(this.xllist1[i].id == 1){
									this.xllist1.splice(0,1);
									this.list1 = this.nllist.concat(this.sglist1,this.xllist1);
								}
								else{
								this.list1 = this.nllist.concat(this.sglist1,this.xllist1);
								}
							}
						}else{
							// this.xllist1 = [];
							this.xllist1.push(e);
							xlarr = this.xllist1.slice(-1);
							this.xllist1 = xlarr;
							this.list1 = this.xllist1.concat(this.sglist1,this.nllist);
						}
					
					}else{
					this.xllist1.splice(this.xllist1.indexOf(e),1);
					this.list1 = this.nllist.concat(this.sglist1,this.xllist1);
					}
			console.log(this.list1)
			},
			close(e){
				if(this.list1.indexOf(e) != -1){
					this.list1.splice(this.list1.indexOf(e),1);
					this.nllist.splice(this.nllist.indexOf(e),1);
					this.sglist1.splice(this.sglist1.indexOf(e),1);
					this.xllist1.splice(this.xllist1.indexOf(e),1);
					// this.arrlist.splice(this.arrlist.indexOf(e),1)
				}
			},
			jump(item,e){
				var that = this;
				var onjs;
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
				that.targetjson.lljl1.push(item)
			},
			jump1(item,e){
				var that = this;
				that.cont = e.currentTarget.dataset.click;
				if(that.cont == item.id){
					item.flage = false
					that.targetjson.wdgz1.push(item)
					uni.showToast({
						icon:"none",
						title:"已关注",
						duration:2000
					})
				}
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
				var that = this;
				// that.cont1 = e.currentTarget.dataset.click;
				// console.log(that.cont1)
				
				// if(that.cont1 == item.id){
					// console.log(item)
					that.targetjson.wdgz1.splice(that.targetjson.wdgz1.indexOf(item),1)
				// }
				item.flage = true;
				uni.removeStorageSync('flage')
				uni.showToast({
					title:'取消关注',
					icon:'none',
					duration:2000
				})
			},
			fiflter(){
				var that = this;
				var nl = [];//截取年龄数组
				var sg = [];//截取身高数组
				var sg1 = [];
				var sg2 = [];//过滤身高数据并赋值数组
				var re1 = [];
				var re2 = [];//过滤年龄数据并赋值数组
				that.show = !that.show;
				let list2 = [];//获取list1的text
					for(let i = 0; i < that.xllist1.length; i++){
					list2.push(that.xllist1[i].text)
					};
				for(let i = 0; i < that.targetjson.data1.length; i++){
					re1 = re1.concat(that.targetjson.data1[i].tag.slice(1,2))
					sg1 = sg1.concat(that.targetjson.data1[i].tag.slice(3))
				};
				for(let i = 0 ; i < re1.length; i++){
					re1[i] = re1[i].replace(/[^0-9]/ig,"")
				};
				for(let i = 0; i < sg1.length; i++){
					sg1[i] = sg1[i].replace(/[^0-9]/ig,"")
				};
				console.log(that.nllist);
				for(let i = 0; i < that.nllist.length; i++){
					nl.push(that.nllist[i].text)
				};
				for(let i = 0; i < that.sglist1.length; i++){
					sg.push(that.sglist1[i].text)
				};
				console.log('list2',list2)
				console.log('that.list1',that.list1);
				console.log('json',that.targetjson.data1)
				console.log('sglist1',that.sglist1)
			 function filterByName1(aim, nameArr) {//单个选项多个数据
					 // return aim.filter(item => item.name == nameArr)
					 if(list2.indexOf("不限") !=-1){
						return that.arrlist = that.targetjson.data1.concat(sg2,re2)
						}else{
							
							if(list2 != ''){
								that.arrlist = []
								for(let i = 0; i < nameArr.length; i++) {
				        that.result.push(aim.find(function(item){
							return (item.tag.indexOf(nameArr[i]) != -1);
						} 
						))
				    }
							}
							
					return that.arrlist = that.arrlist.concat(that.result,re2,sg2)//返回给arrlist数组
						}
				    

				};
				console.log('arrlist',that.arrlist);
				filterByName1(that.targetjson.data1,list2)
				
				for(let j = 0; j < nl.length; j++){
					if(nl[j].indexOf("不限") != -1){
						return that.arrlist = that.arrlist.concat(sg2,re2)
					}
					else {
						that.arrlist = []
						if(nl[j].indexOf("18-20岁") != -1){
						for(let i =0; i < re1.length; i++){
							if(re1[i] >= 18 && re1[i] <= 20){
								re2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(re1[i] + '岁') != -1);
								}))
							}
						}
					}else if(nl[j].indexOf("20-25岁") != -1){
						for(let i =0; i < re1.length; i++){
							if(re1[i] > 20 && re1[i] <= 25){
								re2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(re1[i] + '岁') != -1);
								}))
							}
						}
					}else if(nl[j].indexOf("25-30岁") != -1){
						for(let i =0; i < re1.length; i++){
							if(re1[i] > 25 && re1[i] <= 30){
								re2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(re1[i] + '岁') != -1);
								}))
							}
						}
					}
					else if(nl[j].indexOf("30-35岁") != -1){
						for(let i =0; i < re1.length; i++){
							if(re1[i] > 30 && re1[i] <= 35){
								re2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(re1[i] + '岁') != -1);
								}))
							}
						}
					}
					else if(nl[j].indexOf("35-40岁") != -1){
						for(let i =0; i < re1.length; i++){
							if(re1[i] > 35 && re1[i] <= 40){
								re2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(re1[i] + '岁') != -1);
								}))
							}
						}
					}
					else if(nl[j].indexOf("40-45岁") != -1){
						for(let i =0; i < re1.length; i++){
							if(re1[i] > 40 && re1[i] <= 45){
								re2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(re1[i] + '岁') != -1);
								}))
							}
						}
					}
					else if(nl[j].indexOf("45-50岁") != -1){
						for(let i =0; i < re1.length; i++){
							if(re1[i] > 45 && re1[i] <= 50){
								re2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(re1[i] + '岁') != -1);
								}))
							}
						}
					}
					else if(nl[j].indexOf("50-55岁") != -1){
						for(let i =0; i < re1.length; i++){
							if(re1[i] > 50 && re1[i] <= 55){
								re2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(re1[i] + '岁') != -1);
								}))
							}
						}
					}
					that.arrlist = that.arrlist.concat(sg2,re2)
					}
				};
				for(let k = 0; k < sg.length; k++){
					if(sg[k].indexOf("不限") != -1){
						
						return that.arrlist = that.arrlist.concat(sg2,re2)
					}
					else {
						that.arrlist = []
					if(sg[k].indexOf("156-160cm") != -1){
						for(let i =0; i < sg1.length; i++){
							if(sg1[i] >= 156 && sg1[i] <= 160){
								sg2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(sg1[i] + 'cm') != -1);
								}))
							}
						}
					}else if(sg[k].indexOf("160-165cm") != -1){
						for(let i =0; i < sg1.length; i++){
							if(sg1[i] >160  && sg1[i] <= 165){
								sg2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(sg1[i] + 'cm') != -1);
								}))
							}
						}
					}else if(sg[k].indexOf("165-170cm") != -1){
						for(let i =0; i < sg1.length; i++){
							if(sg1[i] > 165 && sg1[i] <= 170){
								sg2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(sg1[i] + 'cm') != -1);
								}))
							}
						}
					}
					else if(sg[k].indexOf("170-175cm") != -1){
						for(let i =0; i < sg1.length; i++){
							if(sg1[i] > 170 && sg1[i] <= 175){
								sg2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(sg1[i] + 'cm') != -1);
								}))
							}
						}
					}
					else if(sg[k].indexOf("175-180cm") != -1){
						for(let i =0; i < sg1.length; i++){
							if(sg1[i] > 175 && sg1[i] <= 180){
								sg2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(sg1[i] + 'cm') != -1);
								}))
							}
						}
					}
					else if(sg[k].indexOf("180-185cm") != -1){
						for(let i =0; i < sg1.length; i++){
							if(sg1[i] > 180 && sg1[i] <= 185){
								re2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(sg1[i] + 'cm') != -1);
								}))
							}
						}
					}
					else if(sg[k].indexOf("185-190cm") != -1){
						for(let i =0; i < sg1.length; i++){
							if(sg1[i] > 185 && re1[i] <= 190){
								sg2.push(that.targetjson.data1.find(function(item){
									return (item.tag.indexOf(sg1[i] + 'cm') != -1);
								}))
							}
						}
					}
					that.arrlist = that.arrlist.concat(sg2,re2)
					}
				};
				
				// that.arrlist = that.arrlist.concat(re2,sg2)
				for(let i = 0; i < that.arrlist.length; i++){
					for(let j = i+1; j < that.arrlist.length; j++){
						if(that.arrlist[j] == that.arrlist[i]){
							that.arrlist.splice(j,1);
							j--
						}
					}
				}
				console.log('sg1',sg1)
				console.log('sg2',sg2)
				console.log('re2',re2)
				console.log('re1',re1)
				console.log('sg',sg)
				console.log('nl',nl)
				
			}
		}
	}
</script>

<style lang="scss">
	page{
		padding-top: 120rpx;
		background-color: #F1F1F1;
	}
.active{
	
		border-color: #ff3622 !important;
		background-color: #ffa18f !important;
		
	}

	@import '/target.scss';
</style>