<template>
	<view>
		<view class="position-relative d-flex a-center" style="height: 320rpx;">
			<!-- 点击打开消息列表 -->
			<navigator url="../msg-list/msg-list">
				
				<view class="iconfont icon-xiaoxi position-absolute text-white"
				style="font-size: 50rpx;top: 75rpx;right: 20rpx;z-index: 100;">
				</view>
			</navigator>
			<image src="../../static/bg.jpg" mode="widthFix" 
			style="height: 320rpx;"></image>
			<view class="d-flex a-center position-absolute left-0 right-0"
			style="bottom: 50rpx;">
			
			
				<image v-if="userInfo.avatar" :src="userInfo.avatar" @click="navigate('user-info')"
				style="width: 145rpx;height: 145rpx;border: 5rpx solid;" 
				class="rounded-circle border-light ml-4"></image>
				
				<image v-else src="../../static/userpic.png" @click="openLogin"
				style="width: 145rpx;height: 145rpx;border: 5rpx solid;" 
				class="rounded-circle border-light ml-4"></image>
				
				<view class="ml-2 text-white font-md" @click="navigate('user-info')" v-if="userInfo.username">
				{{userInfo.username}}
				</view>
				
				<view class="ml-2 text-white font-md" v-else
				@click="openLogin">登录/注册</view>
				
				<view class="d-flex a-center j-center a-self-end ml-auto pl-1 pr-1" v-show="loginStatus"
				style="height: 70rpx;background: #F0AD4E;color: #CC4A00;
				border-top-left-radius: 40rpx;border-bottom-left-radius: 40rpx;">
					<view class="line-h iconfont icon-huangguan mr-1"></view>
					会员积分 {{userInfo.jifen}}
				</view>
			</view>
		</view>
		<card >
			<view slot="title" class="d-flex a-center j-sb w-100">
				<text class="font-md font-weight">我的订单</text>
				<view class="text-secondary font ml-auto" 
				@click="navigate('order',true)">
					全部订单 <text class="iconfont icon-you font"></text>
				</view>
			</view>
		</card>
		
		<divider></divider>
		<uni-list-item title="会员" showExtraIcon="true" leftIcon="icon-VIP" 
		leftIconStyle="color:#FDBF2E"></uni-list-item>
		
		<divider></divider>
		<uni-list-item title="更多设置" showExtraIcon="true" leftIcon="icon-icon_set_up"
		leftIconStyle="color:#808C98"
		@click="navigate('user-set')"></uni-list-item>
	</view>
	
</template>

<script>
	import uniListItem from "@/components/uni-ui/uni-list-item/uni-list-item.vue"
	import {mapMutations,mapState} from 'vuex';
	export default {
		components:{
			uniListItem
		},
		data() {
			return {
				orders:[
					{
						name:"待付款",
						icon:"icon-wallet_icon",
						index:1
					}
					,{
						name:"待发货",
						icon:"icon-",
						index:1
					}
					,{
						name:"待收货",
						icon:"",
						index:2
					},{
						name:"待评价",
						icon:"icon-pinglun",
						index:3
					},{
						name:"退款",
						icon:"icon-buoumaotubiao46"
					},
				]
			}
		},
		computed:{
			...mapState({
				userInfo:state=>state.user.userInfo,
				loginStatus:state=>state.user.loginStatus
			})
		},
		methods: {
			navigate(path,check = false){
				if(!path) return;
				
				if(check){
					return this.navigateTo({
						url:`/pages/${path}/${path}`
					})
				}
				uni.navigateTo({
					url:`/pages/${path}/${path}`
				})
			},
			openLogin(){
				if(!this.loginStatus){
					uni.navigateTo({
						url:'../login/login'
					})
				}
				
			}
				
		}
	}
</script>

<style>
</style>
