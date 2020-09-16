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
				name:"",
				lat:0,
				long:0,
				fromtype:1  //区分是哪个页面跳转过来得  1是支付功能  2是更换车牌功能
			}
		},
		onLoad(option){
			if(option.platenumber != 'null'){
				this.fromtype = 2;
				this.name = option.name;
				this.lat = option.lat;
				this.long = option.long;
				this.$children[0].getdefaultcarInput(option.platenumber);
			}else{
				this.fromtype = 1;
				this.$children[0].getdefaultcarInput('');
			}
			
			
		},
		methods:{
			confirm:function(){
				var _self=this;
				if(_self.fromtype == 1 ){
					_self.$children[0].toBind(_self.info);
				}else{
					uni.openLocation({
					    latitude:Number(_self.lat),
					    longitude: Number(_self.long),
						address:_self.name,
					    success: function () {
					        console.log('success');
					    }
					});
				}
			},
			cancel:function(){
				console.log("点击了取消按钮");
				uni.navigateBack({
					delta:1
				});
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
					if(_self.carInput[i].val != undefined)
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
			Unumber,
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
