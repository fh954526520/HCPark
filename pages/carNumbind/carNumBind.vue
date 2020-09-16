<template>
	<view class="content">
		<view class="title">
			<text @click="changegoto">请输入完整车牌</text>
		</view>
		<view class="car-num">
			<numbers></numbers>
		</view>
	</view>
</template>
	

<script>
	import numbers from "@/Components/carNum/index.vue"
	export default {
		data(){
			return{
				 CarNo:[], // 写个默认值 ，识别键盘获取的车牌号
				
			}
		},
		methods:{
			
		},
		watch:{
		
		},
		components:{
			numbers
		}
	}
</script>

<style scoped>
	page{
	width: 100%;
	height:100%;
	}
	.content{
		width:  100%;
		position: relative;
	}
	.title{
		font-size:3.5vh;
		color:#0A0A0A;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		margin-top: 10vh;
	}
	.car-num{
		display: flex;
		flex-direction: row;
		flex-shrink:0;
		justify-content: center;
		  
	}
	.input-item{
		height: 90rpx;
		width: 77rpx;
		border:#E1E1E1 solid 1px;
		margin-left: auto;
		margin-right: auto;
		text-align: center;
	}

</style>
