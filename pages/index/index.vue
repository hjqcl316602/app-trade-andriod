<template>
	<view>
		<view style="width: 300upx;height:100upx;background: red;margin-bottom: 20upx;" v-for="(item, index) in 10" :key="index">
			<text style="font-size: 32upx;">{{ item }}我和我祖国</text>
			<text class="icon-test">&#xe60a;</text>
		</view>
		<view style="height:100px;background: blue;margin-bottom: 20px;" v-for="(item, index) in 10" :key="index">{{ item }}</view>
	</view>
</template>

<script>
import { audio } from '../../static/index.js';
export default {
	components: {},
	data() {
		return {
			title: 'Hello'
		};
	},
	onLoad() {},
	methods: {
		playAudio() {
			const innerAudioContext = uni.createInnerAudioContext();
			innerAudioContext.autoplay = true;
			innerAudioContext.src = audio.order; //'../../static/audio/order.mp3'; //'https://img-cdn-qiniu.dcloud.net.cn/uniapp/audio/music.mp3';
			innerAudioContext.onPlay(() => {
				console.log('开始播放');
			});
			innerAudioContext.onError(res => {
				console.log(res.errMsg);
				console.log(res.errCode);
			});
		}
	},
	onNavigationBarButtonTap(e) {
		if (e.float === 'right') {
			uni.navigateTo({
				url: '../user/user'
			});
		}
		console.log(e);
	},
	mounted() {}
};
</script>

<style>
@font-face {
     font-family: "test1-icon";
     src: url('~@/static/icon-font/iconfont.ttf');
 }
 .icon-test{
	 font-family:"test1-icon" ;
	 font-size: 32upx;
 }
.nav-title {
	width: 100%;
	text-align: center;
}
.content {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	background: #fff;
}

.logo {
	height: 200rpx;
	width: 200rpx;
	margin-top: 200rpx;
	margin-left: auto;
	margin-right: auto;
	margin-bottom: 50rpx;
}

.text-area {
	display: flex;
	justify-content: center;
}
</style>
<style lang="scss">
.title {
	color: $uni-bg-color-hover;
	font-size: 12px;
}
</style>
