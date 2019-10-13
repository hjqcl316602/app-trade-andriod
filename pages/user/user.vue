<template>
	<view class="">
		<view class=" vi-background is-background--primary">
			<view class="vi-padding--large vi-padding-top--larger vi-padding-bottom--larger">
				<view class="vi-flex vi-align-items--center">
					<view class="app-head-wrapper vi-margin-right">
						<block v-if="!userMember.avatar">
							<image :src='image.headNormal' class="app-head"></image>
						</block>
						<block v-else>
							<image :src='userMember.avatar' class="app-head"></image>
						</block>
						
					</view>
					<view class="">
						<view>
							<text class="vi-font-size--large vi-color--white vi-font-weight--bold"  >{{ userMember.username }}</text>
						</view>
						<view class="vi-margin-top">
							<text class="vi-color--white">{{ userMember.realName }}</text>
						</view>
					</view>
				</view>
			</view>
		</view> 
		<view class="vi-row vi-border is-border--bottom is-border--thiner"  >
			<view class="vi-span is-span--12 vi-border is-border--right is-border--thiner">
				<view class="vi-padding--large vi-background vi-padding-top--larger vi-padding-bottom--larger">
					<view class="vi-text-align--center">
						 <text style="line-height: 28px;" class="vi-color--light">全部收款</text>
					</view>
					<view class="vi-text-align--center">
						 <text style="line-height: 32px;">
							 <text>￥</text>
							 <text style="font-size: 24px;" class="vi-font-weight--bold">120.00</text>
						 </text>
					</view>
					<view class="vi-text-align--center">
						<view class="vi-btn is-btn--smaller" @click="handler('check','total')" > 
							查看明细
						</view>
					</view>
					
				</view>
			</view>
			<view class="vi-span is-span--12 ">
				<view class="vi-padding--large vi-background vi-padding-top--larger vi-padding-bottom--larger">
					<view class="vi-text-align--center">
						 <text style="line-height: 28px;" class="vi-color--light">今日收款</text>
					</view>
					<view class="vi-text-align--center">
						 <text style="line-height: 32px;">
							 <text>￥</text>
							 <text style="font-size: 24px;" class="vi-font-weight--bold">120.00</text>
						 </text>
					</view>
					<view class="vi-text-align--center">
						<view class="vi-btn is-btn--smaller" > 
							查看明细
						</view>
					</view>
					
				</view>
			</view>
		</view>
		<view class="vi-row vi-border is-border--bottom is-border--thiner">
			<view class="vi-span is-span--8 vi-border is-border--right is-border--thiner" @click="handler('order-success')">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe65d;</text>
					</view>
					<view class="vi-text-align--center ">
						<text class="vi-color--light ">完成订单</text>
					</view>
				</view>
			</view>
			<view class="vi-span is-span--8 vi-border is-border--right is-border--thiner" @click="handler('order-wait')">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe60a;</text>
					</view>
					<view class="vi-text-align--center ">
						<text class="vi-color--light ">未完成订单</text>
					</view>
				</view>
			</view>
			<view class="vi-span is-span--8 " @click="handler('order-cancel')">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe61b;</text>
					</view>
					<view class="vi-text-align--center ">
						<text class="vi-color--light ">取消订单</text>
					</view>
				</view>
			</view>
			
		</view>
		<view class="vi-row vi-border is-border--bottom is-border--thiner">
			<view class="vi-span is-span--6 vi-border is-border--right is-border--thiner">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe674;</text>
					</view>
					<view class="vi-text-align--center ">
						<text class="vi-color--light ">广告</text>
					</view>
				</view>
			</view>
			<view class="vi-span is-span--6 vi-border is-border--right is-border--thiner">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe639;</text>
					</view>
					<view class="vi-text-align--center ">
						<text class="vi-color--light ">账号</text>
					</view>
				</view>
			</view>
			<view class="vi-span is-span--6 vi-border is-border--right is-border--thiner">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe61a;</text>
					</view>
					<view class="vi-text-align--center ">
						<text class="vi-color--light ">钱包</text>
					</view>
				</view>
			</view>
			<view class="vi-span is-span--6">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe604;</text>
					</view>
					<view class="vi-text-align--center ">
						<text class="vi-color--light ">推广</text>
					</view>
				</view>
			</view>
		</view> 
	</view>
</template>

<script>
	import { mapState, mapMutations } from 'vuex';
	import { image } from '../../static/index.js';
export default {
	data() {
		return {
			count: 0,
			image:{
				headNormal:image.headNormal
			}
		};
	},
	computed:{
		...mapState({
			userMember:state=> state.user.member
		})
	},
	mounted() {
		console.log('user-mounted')
	},
	beforeDestroy() { 
	},
	onNavigationBarButtonTap({ float,index}) { 
		if(float === 'right' && index === 0 ){
			uni.navigateTo({
				url:'/pages/set/set'
			})
		}
	},
	methods: {
		handler(handler,type){ 
			uni.navigateTo({
				url:'/pages/set/set'
			})
		}
	}
};
</script>

<style lang="scss"> 
.app-head-wrapper{
	border: 2px solid #fff;
	background: #fff;
	border-radius: 100%;
	overflow: hidden;
}
.app-head {
	height:60px;
	width: 60px; 
	display: block;
} 
</style>
