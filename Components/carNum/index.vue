<template xlang="wxml">
	<view class="body">
		<view class="carinput">
		
			<view class="carinput-input">
				<view class="carinput-input-i" :class="{'input-active':carIndex == i}" @click="inputKey" :data-index="i" v-for="(v,i) in carInput" :key="i" v-show="i < 7">
					<text>{{carInput[i].val}}</text>
				</view>
				<view class="carinput-input-i"style="border:1px solid #2DD661;"  :class="{'input-active':carIndex == 7}" @click="inputKey" data-index="7">
					<view style="width:72upx;border-radius: 10rpx;background-color:#2DD661;height: 25upx; position: absolute;top: 124rpx;border-radius: 11rpx;display: flex; align-items: center;justify-content: center;">
						<view style="color: #FFFFFF;width: ;font-size: 18rpx;">
							<text>新能源</text>
						</view>
					</view>
					<text>{{isPower ? '':'+'}}{{carInput[7].val?carInput[7].val:''}}</text>
				</view>
			</view>
			<view class="carinput-power" style="isplay: flex; flex-direction: row;align-items: center;justify-content: center;">
			   <!-- <checkbox-group class="checkbox-g" @change="powerChange">
					<label class="checkbox">
						<checkbox value="true" :checked="isPower" />
						新能源
					</label>
				</checkbox-group> -->
				<text>切换为新能源车牌</text>
				<switch style="transform: scale(0.8);" :checked="isPower" @change="powerChange" />
			</view>
		</view>
		<view class="card-btn">
			<button class="btn" hover-class="hover-c" type="default" @click="toBind">
				确定
			</button>
		</view>
		<tki-float-keyboard ref="keybd" :mode="'car'" :type="keyType" :title="'特殊车牌'" @del="keyCbDel" @val="keyCbVal" @hide="keyCbHide"></tki-float-keyboard>
	</view>
</template>
<script>
import tkiFloatKeyboard from "@/Components/carNum/tki-float-keyboard/tki-float-keyboard.vue";
export default {
	data() {
		return {
			carIndex: -1,
			carInput: [
				{ type: 2, val: "" },
				{ type: 4, val: "" },
				{ type: 1, val: "" },
				{ type: 1, val: "" },
				{ type: 1, val: "" },
				{ type: 1, val: "" },
				{ type: 3, val: "" },
				{ type: 1, val: "" }
			],
			keyType: 0,
			isPower: false, // 新能源
			platNumber:''
		};
	},
	methods: {
		// 判定是否为空
		empty(v) {
			let tp = typeof v,
				rt = false;
			if (tp == "number" && String(v) == "") {
				rt = true
			} else if (tp == "undefined") {
				rt = true
			} else if (tp == "object") {
				if (JSON.stringify(v) == "{}" || JSON.stringify(v) == "[]" || v == null) rt = true
			} else if (tp == "string") {
				if (v == "" || v == "undefined" || v == "null" || v == "{}" || v == "[]") rt = true
			} else if (tp == "function") {
				rt = false
			}
			return rt
		},
		inputKey(e) {
			let that = this;
			let data = e.currentTarget.dataset;
			if (data.index >= 7) {
				if (!that.isPower) {
					return false;
				} else {
					that.carIndex = 7; 
				}
			} else {
				that.carIndex = data.index;
			}
			that.upKeyType();
			that.keyShow();
		},
		keyCbVal(e) {
			let that = this;
			let index = Number(that.carIndex);
			if (index >= 0 && index < 6) {
				that.carInput[index].val = e;
				that.carIndex = index + 1;
			} else if (index == 6) {
				that.carInput[index].val = e;
				if (that.isPower) {
					// 新能源
					that.carIndex = 7;
				} else {
					// 不是新能源出输入结束
					that.keyHide();
					that.carIndex = -2;
					console.log('非新能源车输入完毕');
					for(let i=0;i<that.carInput.length;i++){
						if(that.carInput[i].val != undefined)
						that.platNumber+=that.carInput[i].val;
					}
				}
			} else if (index == 7) {
				// 新能源车输入完毕
				that.carInput[index].val = e;
				that.keyHide();
				that.carIndex = -3;
				console.log('新能源车输入完毕');
				for(let i=0;i<that.carInput.length;i++){
					if(that.carInput[i].val != undefined)
					that.platNumber+=that.carInput[i].val;
				}
			}
			that.upKeyType();
		},
		keyCbDel(e) {
			let index = this.carIndex;
			if (index > 0) {
				if (!this.empty(this.carInput[index].val)) {
					this.carInput[index].val = "";
					this.carIndex = index;
				} else {
					this.carInput[index - 1].val = "";
					this.carIndex = index - 1;
				}
			}
			this.upKeyType();
		},
		upKeyType() {
			if (!this.empty(this.carInput[this.carIndex])) {
				this.keyType = this.carInput[this.carIndex].type;
			}
		},
		keyShow() {
			this.$refs.keybd._keyShow();
		},
		keyHide() {
			this.$refs.keybd._keyHide();
		},
		keyCbHide() {
			if (this.carIndex != -3 || this.carIndex != -2) {
				this.carIndex = -1;
			}
		},
		powerChange(e) {
		
			let that = this
			let i = that.checkCar().i
			that.isPower =!that.isPower;
			if (that.isPower===true) {
				if (i == -1) {
					that.carIndex = 7;
				} else {
					that.carIndex = i;
				}
				that.keyShow();
			}else {
				that.carInput[7].val = "";
				if (that.carIndex == 7) {
					that.keyHide();
					that.carIndex = -2;
				}
			}
			that.upKeyType();
		},
		checkCar() {
			// 检查车牌是否输入完成
			let that = this;
			let i = 7;
			let rt = { i: -1, isempty: false, val: "" };
			if (that.isPower) {
				i = 8;
			}
			for (let index = 0; index < i; index++) {
				const obj = that.carInput[index];
				if (this.empty(String(obj.val))) {
					rt.i = index;
					rt.isempty = true;
					rt.val = "";
					break;
				}
				rt.val += that.carInput[index].val;
			}
			return rt;
		},
		toBind() {
			let that = this
			let ck = that.checkCar();
			if (ck.i == -1 && !ck.isempty) {
				console.log('可以绑定车牌了');
				console.log(this.platNumber);
				uni.showToast({
					title:"绑定车牌",
					duration:1500
				});
				setTimeout(function(){
					uni.navigateTo({
						url:"../../pages/index/index"
					});
				},1500)
			} else {
				uni.showToast({
					title:"！请重新输入",
					duration:1000,
				})
				that.keyShow();
				that.carIndex = ck.i;
				that.keyType = that.carInput[ck.i].type;
			}
		}
	},
	components: {
		tkiFloatKeyboard
	},
	computed: {},
	watch: {},
	onPageScroll: function () {
		let that = this;
	},
	onReachBottom: function () {
		let that = this;
	},
	onPullDownRefresh: function () {
		let that = this;
	},
	onShow: function () {
		let that = this;
	},
	onHide: function () {
		let that = this;
	},
	onUnload: function () {
		let that = this;
	},
	onLoad: async function () {
		let that = this;
	}
};
</script>

<style>
@import "./style.css";

</style>
