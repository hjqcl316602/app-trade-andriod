<script>
export default {
	onLaunch: function() {
		console.log('App Launch');
		uni.request({
			url: 'http://trade.bstchain.com/uc/check/login',
			method: 'POST',
			success: res => {
				console.log(res.data.data);
				if (res.data.data == null) {
					return false;
					setTimeout(() => {
						uni.navigateTo({
							url: '/pages/login/login'
						});
					}, 3000);
				}
			}
		});
	},
	onShow: function() {
		console.log('App Show');
	},
	onHide: function() {
		console.log('App Hide');
	}
};
</script>

<style lang="scss">
@import 'static/css/store/index.scss';
@import 'static/css/common.scss';
@import 'static/css/main.scss';
</style>
