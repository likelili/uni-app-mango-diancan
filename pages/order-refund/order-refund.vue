<template>
	<view>
		<textarea v-model="reason" placeholder="请填写退款理由" class="uni-textarea p-2"/>
		<view class="p-3">
			<button type="default" class="bg-light" @click="submit"
			:disabled="reason.length === 0" :loading="loading">
				{{loading ? '加载中...' : '申请退款'}}
			</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:0,
				reason:"",
				loading:false
			}
		},
		onLoad(e) {
			if(!e.detail){
				return uni.showToast({
					title: '非法参数',
					icon: 'none'
				});
			}
			this.id = (JSON.parse(e.detail)).id
		},
		methods: {
			submit(){
				this.loading = true
				this.$H.post('/order/order/refund/'+this.id,{
					reason:this.reason
				},{
					token:true
				}).then(res=>{
					this.loading = false
					uni.navigateBack({
						delta: 1
					});
					uni.showToast({
						title: '申请成功，等待商家审核',
						icon: 'none'
					});
				}).catch(err=>{
					this.loading = false
				})
			}
		}
	}
</script>

<style>

</style>
