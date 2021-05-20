<template>
	<view class="">
		<uni-list v-for="(row, index) in tllist" :key="index">
		    <uni-list-item :title="row.type" :note="row.content" :rightText="row.price" to="../detail/detail"></uni-list-item>
		</uni-list>
  </view>
	
</template>

<script>
	export default{
		data(){
			return{
				tllist:[],
			}
		},
		onLoad(option) {
			const that = this
			console.log(option.name)
			uni.showLoading({

			})
			uniCloud.callFunction({
				name:'findtype',
				data:{
					id:'wzj',
					value:option.name
				},
				success(res) {
					console.log(res)
					that.tllist = res.result.data
					that.tllist.forEach((item, index) => {
						if (item.money_type == "日结") {
							item.price = item.price + "/日"
						}
					})
				},
				complete() {
					uni.hideLoading()
				}
			})
		},
		methods:{
		}
	}
</script>

<style>
</style>
