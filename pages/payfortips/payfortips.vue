<template>
	<view class="content">
		<view class="top-image">
			<image src="../../static/images/paydetails/che拷贝4@2x.png" style="width: 120rpx;height: 75rpx;" mode=""></image>
		</view>
		<view class="input-parking-content">
			<text class="font-edi">输入车牌号</text>
			<view>
				<Unumber @getCarInput="getCarInput"></Unumber>
			</view>
		</view>
		<view class="button-group">
				<button type="default" class="btn" @click="confirm">确定</button>
				<button type="default" class="btn"  @click="cancel" style="margin-top: 3vh;">取消</button>
			
		</view>
	</view>
</template>

<script>
	import Unumber from "@/Components/payfortips/index.vue"
	export default{
		data(){
			return{
				carIndex:-1,
				carInput:'',
				info:{},
			}
		},
		methods:{
			confirm:function(){
				console.log("点击了确定按钮");
				var _self=this;
				_self.$children[0].toBind(_self.info);
			},
			cancel:function(){
				console.log("点击了取消按钮");
			uni.navigateTo({
				url:"../index/index",
			})
			},
			getCarInput:function(value){
				var _self=this;
				_self.carInput=value;
				console.log("---------")
				console.log(_self.carInput);
				_self.createobj();
			},
			createobj:function(){
				var _self=this;
				let tipsmessage="";
				for(let i=0;i<_self.carInput.length;i++){
					tipsmessage+=_self.carInput[i].val;
				}
				_self.info.carinfo=tipsmessage;
				_self.info.parkingFee=24;
				_self.info.Arrears=16;
				_self.info.Plnumber="0079";
				_self.info.Einlassdate="2020-05-20";
				_self.info.Einlasstimes="14:11:11";
				var data=new Date();
				_self.info.appearancedate=String(data.getFullYear())+'-'+String((data.getMonth()+1)>=10?(data.getMonth()+1):'0'+(data.getMonth()+1))+'-'+String(data.getDate());
				_self.info.appearancetimes=String(data.getHours())+':'+String(data.getMinutes()>=10 ? data.getMinutes():'0'+data.getMinutes())+':'+String(data.getSeconds()>=10 ? data.getSeconds():'0'+data.getSeconds());
			},
		},
		components:{
			Unumber
		}
	}
</script>

<style scoped>
	page{
		height: 100%;
		width: 100%;
	}
	.content{
		height:100vh;
		width: 100%;
	}
	.top-image{
		width: 100%;
		height: 20vh;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.input-parking-content{
		width:96vw;
		
		height: 20vh;
		margin-left:2vw;
		border-radius: 24rpx;
		box-shadow: 0px 0px 5px #8bc3ff;
		display: flex;
		justify-content: center;
		flex-direction: column;
	}
	.font-edi{
		font-size: 36rpx;
		color: #237FEC;
		letter-spacing: 8rpx;
		margin-top: 2vh; 
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.button-group{
		width: 100%;
		display: flex;
		margin-top: 8vh;
		flex-direction: column;
	}
	.btn{
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 38rpx;
		width: 70vw;
		border-radius: 60rpx;
		background-color: #4482FF;
		color: #FFFFFF;
	}
	.carinput-input {
	    display: flex;
	    justify-content: center;
		height: 5vh;
		margin-top: 2vh;
	}
	
	.carinput-input-i {
	    width: 70rpx;
	    border-width: 2upx !important;
	    border-style: solid;
	    border-color: #BCBCBC;
	    font-size: 36upx;
	    color: #333333;
	    line-height: 1;
	    margin-right: 12upx;
	    padding-bottom: 7upx;
	    text-align: center;
		line-height: normal;
	}
	
	.carinput-input-i:nth-last-child(1) {
	    margin-right: 0
	}
	
	.carinput-input .input-active {
	    border-bottom-width: 2upx !important;
	    border-bottom-style: solid;
	    border-bottom-color: #23CCAB;
	    color: #23CCAB
	}
</style>
