<template>
	<view class="content">
		<view class="car-info">
			<view>
				<image src="../../static/image/paydetails/che4.png" mode="" style="width:60rpx ;height:37rpx;margin-left: 10vw;"></image>
			</view>
			<view>
				<text style="font-size: 38rpx; margin-left: 20vw;">{{carinfo}}</text>
			</view>
		</view>
		<view class="parking-rate">
			<view>
				<text style="font-size: 40rpx;margin-left: 10vw;">停车费:</text>
			</view>
			<view>
				<text style="font-size: 45rpx;color:#FF3300;margin-left: 5vw;">{{parkingFee}}</text>
			</view>
		</view>
		<view class="parking-details">
			<view class="parking-details-row">
				<view class="row-title">
					<text>欠费金额</text>
					<text>:</text>
				</view>
				<view>
					<text style="margin-left: 5vw; color: #4482FF;">{{Arrears}}元</text>
				</view>
				<view>
					<image src="../../static/image/paydetails/3340.png" style="width: 32rpx;height: 32rpx; margin-left: 2vw;" mode=""></image>
				</view>
			</view>
			<view class="parking-details-row">
				<view class="row-title">
					<text>车位号</text>
					<text>:</text>
				</view>
				<view style="margin-left: 5vw;">
					<text>{{Plnumber}}</text>
				</view>
			</view>
			<view class="parking-details-row">
				<view class="row-title">
					<text>入场时间</text>
					<text>:</text>
				</view>
				<view style="margin-left: 5vw;">
					<text>{{Einlassdate}}</text>
				</view>
				<view style="margin-left: 2vw;">
					<text>{{Einlasstimes}}</text>
				</view>
			</view>
			<view class="parking-details-row">
				<view class="row-title">
					<text>出场时间</text>
					<text>:</text>
				</view>
				<view style="margin-left: 5vw;">
					<text>{{appearancedate}}</text>
				</view>
				<view style="margin-left: 2vw;">
					<text>{{appearancetimes}}</text>
				</view>
			</view>
		</view>
		<view class="btn">
			<view class="cancle-btn" @click="cancle">
				<button type="default" style="width: 100%;height: 100%; display: flex; align-items: center; justify-content: center;color: #4482FF; background-color:#FFFFFF ;">取消</button>
			</view>
			<view class="confirm-btn" @click="confirm">
				<button type="default" style="width: 100%;height: 100%; display: flex; align-items: center; justify-content: center;background-color: #4482FF; color: #FFFFFF;">确认</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				carinfo:"渝AMW416",
				parkingFee:"￥7.00",
				Arrears:24,
				Plnumber:"0075",
				Einlassdate:"2020-05-20",
				Einlasstimes:"14:11:11",
				appearancedate:"2020-05-20",
				appearancetimes:"14:11:11",
			}
		},
		methods:{
			cancle:function(){
				console.log("点击了取消按钮");
			},
			confirm:function(){
				console.log("点击了确认按钮");
			}
			
		},
		created() {
			
		},
		comments:{
			
		}
	}
</script>

<style scoped>
 	page{
		width: 100%;
		height: 100% !important;
	}
	.content{
		width: 100%;
		height: 100vh;
		background-color: #F7F7F7;
	}
	.car-info{
		width: 100%;
		height: 10vh;
		display: flex;
		background-color: #FFFFFF;
		flex-direction: row;
		align-items: center;
	}
	.parking-rate{
		width: 100%;
		height: 15vh;
		background-color: #FFFFFF ;
		margin-top: 2vh;
		display: flex;
		flex-direction: row;
		align-items: center;
	
		
	}
	.parking-details{
		width: 100%;
		height: 25vh;
		background-color:#FFFFFF ;
		margin-top: 2vh;
		display: flex;
		flex-direction: column;
		}
	.btn{
		width: 100%;
		height: 8vh;
		margin-top: 5vh;
		display: flex;
		flex-direction: row;
		}
		.parking-details-row{
			display: flex;
			flex-direction: row;
			margin-left:10vw;
			margin-bottom: auto;
			margin-top: auto;
			font-size: 32rpx;
		}
		.row-title{
			width: 20vw;
			text-align: justify;
			text-align-last: justify;
			color: #848484;
		}
		.cancle-btn{
			width:45vw;
			height: 100%;
			border-radius: 4px;
			display: flex;
			align-items: center;
			justify-content: center;
			border: 1px solid #4482FF;
			margin-left: auto;
			margin-right: auto;
		}
		.confirm-btn{
			width:45vw;
			height: 100%;
			border-radius: 4px;
			display: flex;
			align-items: center;
			justify-content: center;
			border: 1px solid #4482FF;
			margin-left: auto;
			margin-right: auto;
		}
</style>
