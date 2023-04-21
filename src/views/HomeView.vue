<template>
	<div class="home">
		<img alt="Vue logo" src="../assets/logo.png">
		<HelloWorld msg="Welcome to Your Vue.js App" />
		<div class="btn-box">
			<van-button type="primary">主要按钮</van-button>
			<van-button type="success">成功按钮</van-button>
			<van-button type="default">默认按钮</van-button>
			<van-button type="warning">警告按钮</van-button>
			<van-button type="danger">危险按钮</van-button>
		</div>
		<van-switch v-model="checked" />
		<van-area title="标题" :area-list="areaList" :columns-num="3" :value="areaVal" @confirm="getAreaList" />
		<div class="test_two_box">
			<video id="myVideo" class="video-js">
				<source src="//vjs.zencdn.net/v/oceans.mp4" type="video/mp4">
				<source src="//vjs.zencdn.net/v/oceans.webm" type="video/webm">
			</video>
		</div>
	</div>
</template>

<script>
	// @ is an alias to /src
	import HelloWorld from '@/components/HelloWorld.vue'
	import 'video.js/dist/video-js.css'
	import {
		showToast,
		showNotify
	} from 'vant';
	import 'vant/es/toast/style';
	import 'vant/es/notify/style';
	import {
		areaList
	} from '@vant/area-data';
	import video from 'video.js'


	export default {
		name: 'HomeView',
		components: {
			HelloWorld
		},
		setup() {
			return {
				areaList
			};
		},
		data() {
			return {
				checked: true,
				player: null,
				areaVal: ''
			}
		},
		created(){
			console.log("我进来了01")
		},
		mounted() {
			console.log("我进来了01-2")
			showToast({
				message: '顶部展示',
				position: 'top'
			});
			showNotify({
				type: 'success',
				message: '通知内容'
			});
			this.initVideo();
		},
		methods: {
			initVideo() {
				//初始化视频方法
				this.player = video('myVideo', {
					//确定播放器是否具有用户可以与之交互的控件。没有控件，启动视频播放的唯一方法是使用autoplay属性或通过Player API。
					controls: true,
					//自动播放属性,muted:静音播放
					autoplay: "muted",
					//建议浏览器是否应在<video>加载元素后立即开始下载视频数据。
					preload: "auto",
					//设置视频播放器的显示宽度（以像素为单位）
					width: "800px",
					//设置视频播放器的显示高度（以像素为单位）
					height: "400px",
					//播放倍数
					playbackRates: [0.5, 1.0, 1.5, 2.0], // 可选的播放速度
				}, function() {
					this.play()
				});
			},
			getAreaList(val) {
				console.log(val)
				console.log(this.areaVal)
			}
		},
		beforeUnmount() {
			if (this.player != null) {
				this.player.dispose();
			}
		}

	}
</script>

<style scoped>
	.btn-box {
		display: flex;
		justify-content: space-around;
		width: 800px;
		margin: 20px auto;
	}
</style>