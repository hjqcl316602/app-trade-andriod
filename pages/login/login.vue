<template>
	<view>
		<view class="vi-margin-bottom--large ">
			<view class="vi-text-align--center "><text style="font-size: 20px;line-height: 100px;">欢迎登录TTM</text></view>
			<view class="vi-background vi-border is-border--top is-border--thiner">
				<view class=" vi-border is-border--bottom is-border--thiner vi-padding-left--large vi-padding-right--large">
					<view class="vi-input is-input--larger is-input--require" style="line-height: 44px;">
						<view class="vi-text-align--left " style="width:40px"><text>账号</text></view>
						<input type="text" placeholder="请输入您的账号" v-model="params.username" />
					</view>
				</view>
				<view class=" vi-border is-border--bottom is-border--thiner vi-padding-left--large vi-padding-right--large">
					<view class="vi-input is-input--larger is-input--require" style="line-height: 44px;">
						<view class="vi-text-align--left " style="width:40px"><text>密码</text></view>
						<input type="password" placeholder="请输入您的密码" v-model="params.password" />
					</view>
				</view>
				<view class=" vi-border is-border--bottom is-border--thiner vi-padding-left--large vi-padding-right--large" @click="showLoginRememberType">
					<view class="vi-flex vi-padding-left" style="line-height: 44px;">
						<view class="vi-text-align--left " style="width:40px"><text>方式</text></view>
						<view class="vi-flex--1 vi-padding-left vi-padding-right">
							<view class="vi-flex vi-justify-content--space-between">
								<view>
									<text class="vi-color--light">{{ getLoginRememberTypeText(loginRememberType) }}</text>
								</view>
								<view><text class="app-icon  vi-color--gray">&#xe61f;</text></view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>

		<view class=""><view class="vi-btn is-btn--pack is-btn--primary is-btn--long is-btn--larger" @click="loginIn">登录</view></view> 
	</view>
</template>

<script>
import { mapState, mapMutations } from 'vuex';
import request from '../../request/index.js';
import { loginRememberTypes } from '../../config/enumeration.js';

let loginRememberTypeText = [];

loginRememberTypes.forEach(ele => {
	loginRememberTypeText.push(ele.text);
});

export default {
	data() {
		return {
			params: {
				username: '',
				password: ''
			}
		};
	},
	computed: {
		...mapState({
			loginMessage: state => {
				return state.login.message;
			},
			loginRememberType: state => state.login.rememberType
		})
	},
	watch: {
		loginMessage: {
			handler(val) {
				this.params.username = val.username;
				this.params.password = val.password;
			},
			deep: true,
			immediate: true
		}
	},
	methods: {
		...mapMutations({
			setMember: 'setMember',
			setLoginMessage: 'setLoginMessage',
			setLoginRememberType: 'setLoginRememberType'
		}),
		init() {},
		getLoginRememberTypeText(value) {
			let find = loginRememberTypes.find(ele => {
				return ele.value === value;
			});
			return find ? find.text : '';
		},
		showLoginRememberType() {
			uni.showActionSheet({
				itemList: loginRememberTypeText,
				success: ({ tapIndex }) => {
					this.setLoginRememberType(loginRememberTypes[tapIndex].value);
				}
			});
		},
		loginIn() { 
			request('uc/login', this.params, { load: false, loadTitle: '登录中...' }).then(res => {
				if (res.code === 0) { 
					if (this.loginRememberType === 'remember:username') {
						this.setLoginMessage({ username: this.params.username, password: '' })
					} else if (this.loginRememberType === 'remember:usernameAndPassword') {
						this.setLoginMessage({ username: this.params.username, password: this.params.password })
					} else if (this.loginRememberType === 'remember:none') {
						this.setLoginMessage({ username: '', password: '' })
					} 
					let data = res.data || {};
					if(data.token){
						uni.setStorageSync('app/login/token', data.token);
						this.setMember(res.data);
						uni.navigateBack();
						
						uni.showToast({
							title: '登录成功',
							icon: 'success'
						});
					}  
				} else {
					uni.showToast({
						title: res.message,
						icon: 'none'
					});
				}
			});
		}
	}
};
</script>

<style></style>
