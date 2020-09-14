
<template>
    <view class="content">
		<view class="header-content">
			<view class="left-nav" @click="orderChange(1)">
					<text v-bind:class="{'border-show': border ? true:false}" style="width: auto;height: 100%;display: flex;justify-content: center;align-items: center;">所有订单</text>
			</view>
			<view class="middle-nav"></view>
			<view class="right-nav" @click="orderChange(2)">
					<text v-bind:class="{'border-show': border ? false:true}" style="width: auto; height: 100%;	display: flex;justify-content: center;align-items: center;">待支付</text>
			</view>
		</view>
		<view class="all-orders" v-if="allOrder">
			<view class="order-items-content">
				<view class="items" v-for="(item,index) in 15" :key="index">
					<view class="items-left">
						<view style="margin-left: 5vw;display: flex;flex-direction: column;">
							<text v-bind:style="{color:IFpay ? '#FF3300':''}">{{moeny}}元</text>
							<text style="font-size: 24rpx;color: #E4E4E4;">{{address}}</text>
						</view>
					</view>
					<view class="items-right">
						<view>
							<text>{{date}}</text>
							<text style="margin-left: 2vw;">{{times}}</text>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="tobepaid-orders" v-else>
			<view class="order-items-content">
				<view class="items" v-for="(item,index) in 15" :key="index">
					<view class="items-left">
						<view style="margin-left: 5vw;display: flex;flex-direction: column;">
							<text v-bind:style="{color:IFpay ? '#FF3300':''}">{{moeny}}元</text>
							<text style="font-size: 24rpx;color: #E4E4E4;">{{address}}</text>
						</view>
					</view>
					<view class="items-right">
						<view>
							<text>{{date}}</text>
							<text style="margin-left: 2vw;">{{times}}</text>
						</view>
					</view>
				</view>
			</view>
		</view>
    </view>
</template>

<script>
	export default {
	    data() {
	        return {
	           allOrder:true,
			   border:true,
			   moeny:7,
			   address:"合川区xx万华路",
			   IFpay:true,
			   date:"19-09-03",
			   times:"15-27-03"
	        }
	    },
	    methods: {
	        orderChange:function(val){
				var _self=this;
				if(val===1){
					_self.border=true;
					_self.allOrder=true;
				}
				if(val===2){
					_self.border=false;
					_self.allOrder=false;
				}
				
				
				
			},
	        
	    }
	}
</script>

<style scoped>
	page{
		width: 100%;
		height: 100%;
	}
	.content{
		height: 100%;
		width: 100%;
		background-color: #F3F3F3;
	}
	.header-content{
		height: 7vh;
		width: 100%;
		background-color:#FFFFFF ;
		display: flex;
		justify-content: center;
		align-items: center;
		color:#666666;
	}
	.all-orders{
		height:91vh;
		width: 100%;
		margin-top: 2vh;
		background-color:#FFFFFF;
	}
	.tobepaid-orders{
		height: 91vh;
		width: 100%;
		margin-top: 2vh;
		background-color: #FFFFFF;
	}
	.left-nav{
		width: 49.75%;
		height: 100%;
		float: left;
		font-size: 3vh;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.middle-nav{
		width: 0.5%;
		float: left;
		background-color:#666666;
		height: 80%;
	}
	.right-nav{
		width: 49.75%;
		height: 100%;
		float: left;
		font-size: 3vh;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.border-show{
		border-bottom: 2px solid #4482FF;
		color: #4482FF;
	}
	.order-items-content{
		width: 100%;
		height: 100%;
		overflow-y: auto;
	}
	.items{
		width: 100%;
		height: 10vh;
		border: #E4E4E4;
		border-bottom: solid 1px #CCCCCC;
	}
	.items-left{
		width: 50%;
		height: 100%;
		float: left;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
	.items-right{
		width: 50%;
		height: 100%;
		display: flex;
		justify-content: center;
		font-size: 3.5vw;
		align-items:center;
		color: #666666;
		font-weight:500; 
	}
</style>
