<template>
	<view class="content">
		<carousel :img-list="imgList" url-key="url" @selected="selectedBanner"/>
		<view class="category-list">
			<view
				class="category"
				v-for="(row, index) in categoryList"
				:key="index"
				@tap="toCategory(row)"
			>
				<view class="img"><image :src="row.img"></image></view>
				<view class="text">{{ row.name }}</view>
			</view>
		</view>
		<button @click="toFa">fabu</button>
	</view>
</template>

<script>
	import carousel from '@/components/vear-carousel/vear-carousel'
	export default {
		components: {
			carousel
			},
		data() {
			return {
				categoryList: [
					{ id: 1, name: '外卖', img: '/static/img/category/1.png' },
					{ id: 2, name: '快递', img: '/static/img/category/2.png' },
					{ id: 3, name: '家教', img: '/static/img/category/3.png' },
					{ id: 4, name: '零工', img: '/static/img/category/4.png' },
					{ id: 5, name: '在线', img: '/static/img/category/5.png' },
					{ id: 6, name: '运动', img: '/static/img/category/6.png' },
					{ id: 7, name: 'kk', img: '/static/img/category/7.png' },
					{ id: 8, name: 'aa', img: '/static/img/category/8.png' }
				],
				imgList: [{
					url: 'https://img9.51tietu.net/pic/2019-091200/vgkpidei2tjvgkpidei2tj.jpg',
					id: 1,
					},{
					url: 'https://img9.51tietu.net/pic/2019-091200/euzekmi5m23euzekmi5m23.jpg',
					id: 2,
					},{
					url: 'https://img9.51tietu.net/pic/2019-091200/143tt0ta4sr143tt0ta4sr.jpg',
					id: 3,
					},{
					url: 'https://img9.51tietu.net/pic/2019-091200/ff1vqwm3q33ff1vqwm3q33.jpg',
					id: 4,
					},
				]
			}
		},
		methods: {
			toCategory(e) {
				//uni.showToast({title: e.name,icon:"none"});
				uni.setStorageSync('catName',e.name);
				console.log(e.name)
				uni.navigateTo({
					url:"../list/list?cid="+e.id+'&name='+e.name
				});
			},
			selectedBanner(item, index) {
				console.log('', item, index)
			},
			toFa:function() {
				uni.navigateTo({
					url:'../recruit/recruit'
				})
			}
		}
	}
</script>

<style lang="scss">
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	
	.category-list {
		width: 92%;
		margin: 0 4%;
		padding: 0 0 30upx 0;
		border-bottom: solid 2upx #f6f6f6;
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
		.category {
			width: 25%;
			margin-top: 50upx;
			display: flex;
			flex-wrap: wrap;
			.img {
				width: 100%;
				display: flex;
				justify-content: center;
				image {
					width: 9vw;
					height: 9vw;
				}
			}
			.text {
				margin-top: 16upx;
				width: 100%;
				display: flex;
				justify-content: center;
				font-size: 24upx;
				color: #3c3c3c;
			}
		}
	}
</style>

