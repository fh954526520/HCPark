<template>
	<view class="con">
		<mapIndex ref="map" id="map1"  :latitude="latitude" :longitude="longitude"></mapIndex>
	</view>
</template>

<script>
	import mapIndex from '../../Components/map.nvue'
	export default {
		components:{
			mapIndex
		},
		data() {
			return {
				latitude:29.556767,
				longitude:106.463860,
				id:0,
			}
		},
		onLoad(option) {
			console.log(option.id)
		},
		onShow() {
			if(this.id > 0){
				this.$refs.map.searchId(this.id);
			}
			
		},
		methods: {

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
		position: relative;
	}
	#map1{
		height: 100%;
		width: 100%;
	}
	
</style>
