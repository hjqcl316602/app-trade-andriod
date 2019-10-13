<template>
	<view>
		<view class="vi-margin-bottom">
			<view class="vi-border is-border--bottom is-border--thiner vi-background">
				<view class="vi-flex vi-justify-content--space-between vi-padding-left--large vi-padding-right--large" @click="show" style="line-height: 44px;">
					<text>切换账号</text>
					<text class="app-icon vi-color--gray">&#xe61f;</text>
				</view>
			</view>
			<view class="vi-border is-border--bottom is-border--thiner vi-background">
				<view class="vi-flex vi-justify-content--space-between vi-padding-left--large vi-padding-right--large" @click="showOrderNotice" style="line-height: 44px;">
					<text class="">订单语音提醒间隔</text>
					<text >
						<text class="vi-color--gray  vi-margin-right">{{ orderNoticeText }}</text>
						<text class="app-icon  vi-color--gray">&#xe61f;</text>
					</text>
				</view>
			</view>
			<view class="vi-border is-border--bottom is-border--thiner vi-background">
				<view class="vi-flex vi-justify-content--space-between vi-padding-left--large vi-padding-right--large" style="line-height: 44px;">
					<text>资金密码</text>
					<text class="app-icon vi-color--gray">&#xe61f;</text>
				</view>
			</view>
		</view>
		<view class="vi-border is-border--bottom is-border--top is-border--thiner ">
			<view class="vi-btn is-btn--pack is-btn--white is-btn--long is-btn--larger" @click="loginOut">退出登录</view>
		</view>
		<text>{{ userList }}</text>
	</view>
</template>

<script>
import { mapState, mapMutations } from 'vuex';
import request from '../../request/index.js'
let orderNotices = [
	{ text : '5秒' , value : 5 * 1000 },
	{ text : '10秒' , value : 10 * 1000 },
	{ text : '20秒' , value : 20 * 1000 },
	{ text : '30秒' , value : 30 * 1000 },
	{ text : '1分' , value : 60 * 1000 }, 
]

let orderNoticeTexts = []

orderNotices.forEach(ele=>{
	orderNoticeTexts.push(ele.text)
})

export default {
	data() {
		return {};
	},
	computed: {
		...mapState({
			orderNoticeText: state => {
				let find = orderNotices.find((ele)=>{
					return ele.value === state.order.notice
				})
				return find ? find.text : '从不'
			},
			userList : state => {
				console.log(state.user)
				return state.user.list
			}
		})
	},
	methods: {
		...mapMutations({
			setOrderNotice: 'setOrderNotice', 
			setMember:'setMember'
		}),
		
		showOrderNotice() { 
			uni.showActionSheet({
				itemList: orderNoticeTexts,
				success: ({ tapIndex }) => {
					console.log(orderNotices[tapIndex]);
					this.setOrderNotice(orderNotices[tapIndex].value);
				}
			});
		},
		loginOut(){
			request('uc/loginout').then(res=>{
				console.log(res)
				if(res.code === 0 ){
					this.setMember(null)
					uni.showToast({
						title:res.message
					})
					uni.redirectTo({
						url:'/pages/login/login'
					})
				}else{
					uni.showToast({
						title:res.message
					})
				}
			})
		},

		show() {
			uni.showLoading({
				title: '加载中'
			});

			setTimeout(() => {
				uni.hideLoading();
			}, 3000);

			// uni.showModal({
			//     title: '提示',
			//     content: '这是一个模态弹窗',
			//     success: function (res) {
			//         if (res.confirm) {
			//             console.log('用户点击确定');
			//         } else if (res.cancel) {
			//             console.log('用户点击取消');
			//         }
			//     }
			// });
			// uni.showActionSheet({
			//     itemList: ['A', 'B', 'C'],
			//     success: function (res) {
			//         console.log('选中了第' + (res.tapIndex + 1) + '个按钮');
			//     },
			//     fail: function (res) {
			//         console.log(res.errMsg);
			//     }
			// });
		}
	}
};
</script>

<style></style>
