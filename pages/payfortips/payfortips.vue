<template>
	<view class="content">
		<view class="top-image">
			<image src="../../static/image/paydetails/che拷贝4@2x.png" style="width: 120rpx;height: 75rpx;" mode=""></image>
		</view>
		<view class="input-parking-content">
			<text class="font-edi">输入车位号</text>
			<view class="carinput-input">
				<view class="carinput-input-i" :class="{'input-active':carIndex == i}" @tap="inputKey" :data-index="i" v-for="(item,i) in 8" :key="i" >
					1
				</view>
			</view>
		</view>
		<view class="button-group">
				<button type="default" class="btn" @click="confirm">确定</button>
				<button type="default" class="btn" @click="cancel" style="margin-top: 3vh;">取消</button>
			
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				carIndex:-1,
			}
		},
		methods:{
			confirm:function(){
				console.log("点击了确定按钮");
			},
			cancel:function(){
				console.log("点击了取消按钮");
			}
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
	    width: 50upx;
	    border-bottom-width: 2upx !important;
	    border-bottom-style: solid;
	    border-bottom-color: #BCBCBC;
	    font-size: 36upx;
	    color: #333333;
	    line-height: 1;
	    margin-right: 12upx;
	    padding-bottom: 7upx;
	    text-align: center
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
