<script>
	export default {
		globalData:{
			userInfo:{},  //定义用户信息
			config:{
			  key: 'PIBBZ-L2LW6-S6US2-EWJYW-RFWFE-V4BX6',
			  url:'https://apis.map.qq.com/ws/direction/v1/walking/?'
			}//地图配置
		},
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	.left{
		float: left;
	}
	.right{
		float: right;
	}
	.clearfix{
		clear: none;
	}
</style>
