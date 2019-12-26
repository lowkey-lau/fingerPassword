<template>
	<view class="pages">
		<view class="main">
			<view class="link" @click="jump('../setting/setting')">跳转到设置页</view>
			<view class="infoBox">{{ userNameStr }} 你好！</view>
			<view class="titleBox">这是示范登录的</view>
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
			handPsw: '',
			area: '86',
			password: '',
			userNameStr: 'XXX',
			disabled: true
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
			this.handPsw = data.join('');
			
			console.log('当前输入的手势密码是：' + this.handPsw);

			if (this.handPsw == uni.getStorageSync('gesturePsw')) {
				uni.showToast({
					title: '登陆成功',
					icon: 'none'
				});
			} else {
				uni.showToast({
					title: '密码不正确',
					icon: 'none'
				});
			}
		}
	}
};
</script>

<style lang="scss" scoped>
* {
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

.link {
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

.moreBox {
	position: absolute;
	bottom: 30upx;
	left: 50%;
	transform: translateX(-50%);
	color: #333;
	font-size: 32upx;
}
</style>
