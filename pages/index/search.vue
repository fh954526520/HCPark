<template>
	<view class="con">
		<view class="search_head">
			<view class="search_head_input">
				<view class="search_head_input_image left" style="margin-left: 9px;">
					<image src="../../static/images/map/cancel.png" />
				</view>
				<view class="search_head_input_text left">
					<input class="search_input" :value="inputValue" placeholder="请输入车场名称" @input="getInput" />
				</view>
				<view class="search_head_input_image right" style="margin-right: 9px;" @click="clearInput">
					<image src="../../static/images/map/search1.png" />
				</view>
			</view>
			<view class="searchClick" @click="searchInput">
				<span>搜索</span>
			</view>
		</view>
		<scroll-view class="search_list" scroll-y="true" :style="{'height':height+'px'}">
			<view class="park_list" v-for="(item,index) in parklist" @click="getDetail(item.id)" :key="index">
				<span class="left" style="margin-left: 16px;">{{item.name}}</span>
				<span class="right" style="margin-right: 16px;">剩余:{{item.parkcount}}个</span>
			</view>
			
		</scroll-view>
	</view>
</template>

<script>
	import markerData from "../../static/jsData/map.js"
	export default{
		data(){
			return{
				parklist:[],
				inputValue:"",
				height:0,
			}
		},
		created() {
			var _self = this;
			// this.parklist = markerData.markerDetail;	
			uni.getSystemInfo({
			    success: function (res) {
			        var heigit = res.windowHeight;
			        _self.height = heigit-45;
			    }
			});
		},
		onLoad() {
			
		},
		methods:{
			getInput: function(event){
				this.inputValue = event.detail.value;
				var string = "三峡广场";
				
				if(string.indexOf(event.detail.value) != -1 && event.detail.value !=""){
					this.parklist = markerData.markerDetail;
				}else if(event.detail.value !=""){
					this.checkData(event.detail.value);
				}else{
					this.parklist =[];
				}
			},
			/**
			 * @param {Object} data
			 * 查找是否存在当前字符段
			 */
			checkData(data){
				var list = markerData.markerDetail;
				var newlist = [];
				for(var i = 0; i<list.length;i++){
					if(list[i].name.indexOf(data) != -1){
						newlist.push(list[i]);
					}
				}
				this.parklist = newlist;
			},
			/**
			 * 手动搜索
			 */
			searchInput(){
				var string = "三峡广场";
				if(string.indexOf(this.inputValue) != -1 && this.inputValue !=""){
					this.parklist = markerData.markerDetail;
				}else if(this.inputValue !=""){
					this.checkData(this.inputValue);
				}else{
					this.parklist =[];
				}
			},
			clearInput(){
				this.inputValue = "";
				this.parklist = [];
			},
			getDetail(id){
				// let pages = getCurrentPages();  //获取所有页面栈实例列表
				// let nowPage = pages[ pages.length - 1];  //当前页页面实例
				// let prevPage = pages[ pages.length - 2 ];  //上一页页面实例
				// prevPage.$vm.id = id;   //修改上一页data里面的id参数值为id
				// uni.navigateBack({
				// 	delta:1
				// })
				var _self = this;
				if(_self.parklist.length > 0){
					console.log(_self.parklist.length);
					for(var i=0; i<_self.parklist.length;i++){
						
						if(_self.parklist[i].id == id){
							uni.openLocation({
							    latitude:Number(_self.parklist[i].latitude),
							    longitude: Number(_self.parklist[i].longitude),
								address:_self.parklist[i].name,
							    success: function () {
							        console.log('success');
							    }
							});
							break;
						}
						console.log(_self.parklist[i])
					}
				}
			}
		}
	}
</script>

<style>
	page{
		height: 100%;
		width: 100%;
	}
	.con{
		height: 100%;
		width: 100%;
	}
	.search_head{
		height: 45px;
		width: 100%;
		background-color: #E9EBEC;
		position: relative;
	}
	.search_head_input{
		height: 29px;
		top: 8px;
		width: 80%;
		left: 3%;
		background-color: #FFFFFF;
		position: absolute;
	}
	.search_head_input_image{
		height: 16px;
		width: 16px;
		margin-top: 4.5px;
	}
	.search_head_input_image image{
		height: 100%;
		width: 100%;
		
	}
	.search_head_input_text{
		height: 28px;
		width: 60%;
		line-height: 28px;
		font-size: 14px;
		margin-left: 10px;
		margin-top: 3px;
	}
	.search_input{
		
	}
	.searchClick{
		height: 29px;
		width: 15%;
		color: #FC545A;
		line-height: 29px;
		position: absolute;
		right: 1%;
		font-size: 14px;
		top: 8px;
		text-align: center;
	}
	.search_list{
		/* height: 456px; */
		width: 100%;
		/* border: 1px solid red; */
	}
	.park_list{
		height: 40px;
		line-height: 40px;
		width: 100%;
		font-size: 14px;
		color: #8A959E;
		border-bottom: 1px solid #E9EBEC;
		
	}
</style>
