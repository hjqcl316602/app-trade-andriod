<template>
	<view class="">
		<view class=" vi-background is-background--primary">
			<view class="vi-padding--large">
				<view class="vi-flex vi-align-items--center">
					<view class="app-head-wrapper vi-margin-right">
						<image src='../../static/icon/icon-buy-normal.png' class="app-head"></image>
					</view>
					<view class="">
						<view>
							<text class="vi-font-size--large vi-color--white vi-font-weight--bold"  >何事秋风悲画扇</text>
						</view>
						<view class="vi-margin-top">
							<text class="vi-color--white">黄军泉</text>
						</view>
					</view>
				</view>
			</view>
		</view> 
		<view class="vi-row vi-border is-border--bottom is-border--thiner"  >
			<view class="vi-span is-span--12 vi-border is-border--right is-border--thiner">
				<view class="vi-padding--large vi-background">
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
				<view class="vi-padding--large vi-background ">
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
			<view class="vi-span is-span--12 vi-border is-border--right is-border--thiner">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe61b;</text>
					</view>
					<view class="vi-text-align--center vi-margin-top">
						<text class="vi-color--light">全部订单</text>
					</view>
				</view>
			</view>
			<view class="vi-span is-span--12">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe60a;</text>
					</view>
					<view class="vi-text-align--center vi-margin-top">
						<text class="vi-color--light">未完成订单</text>
					</view>
				</view>
			</view>
		</view>
		<view class="vi-row vi-border is-border--bottom is-border--thiner">
			<view class="vi-span is-span--6 vi-border is-border--right is-border--thiner">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe61b;</text>
					</view>
					<view class="vi-text-align--center vi-margin-top">
						<text class="vi-color--light">广告</text>
					</view>
				</view>
			</view>
			<view class="vi-span is-span--6 vi-border is-border--right is-border--thiner">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe61b;</text>
					</view>
					<view class="vi-text-align--center vi-margin-top">
						<text class="vi-color--light">账号</text>
					</view>
				</view>
			</view>
			<view class="vi-span is-span--6 vi-border is-border--right is-border--thiner">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe61b;</text>
					</view>
					<view class="vi-text-align--center vi-margin-top">
						<text class="vi-color--light">钱包</text>
					</view>
				</view>
			</view>
			<view class="vi-span is-span--6">
				<view class="vi-padding--large vi-background">
					<view class="vi-text-align--center">
						<text class="app-icon vi-color--primary" style="font-size: 24px;">&#xe60a;</text>
					</view>
					<view class="vi-text-align--center vi-margin-top">
						<text class="vi-color--light">推广</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			count: 0
		};
	},
	mounted() {},
	beforeDestroy() { 
	},
	onNavigationBarButtonTap({ float,index}) {
		console.log(float,index) 
		if(float === 'right' && index === 0 ){
			uni.navigateTo({
				url:'/pages/set/set'
			})
		}
	},
	methods: {
		handler(handler,type){
			console.log(handler,type)
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
