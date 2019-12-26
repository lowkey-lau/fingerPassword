<template>
	<view class="pages">
		<view class="main">
			<view class="link" @click="jump('../login/login')">跳转到登录页</view>
			<view class="titleBox">绘制解锁图案</view>
			<view class="uni-padding-wrap uni-common-mt">
				<view><mpvue-gesture-lock :containerWidth="590" :cycleRadius="40" @end="onEnd" :password="gesturePassword"></mpvue-gesture-lock></view>
				<!-- <view class="uni-helllo-text uni-common-mt uni-center">你的密码是:   {{handPsw}}</view> -->
			</view>
		</view>
	</view>
</template>

<script>
import mpvueGestureLock from '../../components/mpvueGestureLock/index.vue';

export default {
	components: {
		mpvueGestureLock
	},
	data() {
		return {
			gesturePassword: [],
			handPsw: ''
		};
	},
	onShow() {
		console.log('当前本地存储的手势密码是：' + uni.getStorageSync('gesturePsw'));
	},
	methods: {
		jump(url) {
			uni.navigateTo({
				url: url
			});
		},
		onEnd(data) {
			let that = this;
			that.handPsw = data.join('');

			if (that.gesturePassword.length) {
				if (that.gesturePassword.join('') === data.join('')) {
					uni.setStorage({
						key: 'gesturePsw',
						data: that.handPsw
					});

					console.log('设置成功，当前本地存储的手势密码是：' + uni.getStorageSync('gesturePsw'));
				} else {
					uni.showToast({
						title: '两次密码设定不一致，请重新输入',
						icon: 'none'
					});
					// that.$tools.toast('两次手势密码设定不一致');
					// that.text = '两次手势设定不一致'
					that.gesturePassword = [];
				}
			} else {
				uni.showToast({
					title: '请再次确认手势密码',
					icon: 'none'
				});
				// that.$tools.toast('请确认手势密码设定');
				// that.text = '请确认手势设定'
				that.gesturePassword = data;
			}
		}
	}
};
</script>

<style lang="scss" scoped>
*{
    box-sizing: border-box;
}	
	
.pages {
	background-color: #fff;
}

.main {
	padding: 60upx 0;
	display: flex;
	align-items: center;
	flex-direction: column;
	justify-content: center;
}

.link{
	font-size: 24upx;
	color: $globalColor-light;
	text-align: right;
	width: 100%;
	margin-bottom: 30upx;
	padding: 0 30upx;
}

.logo {
	// width: 60upx;
	display: block;
	text-align: center;
	margin-bottom: 30upx;
	image {
		width: 160upx;
		display: block;
		margin: 0 auto;
	}
}

.infoBox {
	text-align: center;
	font-size: 48upx;
	color: #333;
	margin-bottom: 100upx;
}

.titleBox {
	// padding: 60upx 0;
	text-align: center;
	color: #333;
	font-size: 32upx;
	margin-bottom: 60upx;
}
</style>
