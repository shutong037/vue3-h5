<template>
  <div class="about">
    <h1>This is an about page</h1>
	<div class="btn-box">
		<van-button type="primary">主要按钮</van-button>
		<van-button type="success">成功按钮</van-button>
		<van-button type="default">默认按钮</van-button>
		<van-button type="warning" @click="showTip2">警告按钮</van-button>
		<van-button type="danger" @click="showTip">危险按钮</van-button>
	</div>
	<van-progress :percentage="50" />
	<van-divider />
	
	<van-circle
		v-model:current-rate="currentRate"
		:rate="30"
		:speed="100"
		:text="text"
	/>
	
  </div>
</template>

<script>
	import {
		showNotify,
		showDialog,
		showConfirmDialog
	} from 'vant';
	import 'vant/es/dialog/style'
	import 'vant/es/notify/style'
	import { 
		ref,
		computed
	} from 'vue';
	export default {
		name: 'AboutView',
		data(){
			return {
			
			}
		},
		created(){
			console.log("我进来了02")
		},
		mounted(){
			console.log("我进来了02-2")
			showNotify({
				type: 'danger',
				message: '通知内容'
			});
		},
		methods:{
			showTip(){
				// 判断元素是否存在
				showDialog({
					title: '标题',
					message: '代码是写出来给人看的，附带能在机器上运行。',
				}).then(() => {
					// on close

				});
				
				showDialog({
					message: '生命远不止连轴转和忙到极限，人类的体验远比这辽阔、丰富得多。',
				}).then(() => {
					// on close
				});
			},
			showTip2(){
				showConfirmDialog({
					title: '标题',
					message:
					'如果解决方法是丑陋的，那就肯定还有更好的解决方法，只是还没有发现而已。',
				})
				.then(() => {
					// on confirm
				})
				.catch(() => {
					// on cancel
				});
			}
		},
		setup() {
			const currentRate = ref(0);
			const text = computed(() => currentRate.value.toFixed(0) + '%');
			return {
				text,
				currentRate,
			};
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