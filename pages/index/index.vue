<template>
	<view class="">
		<view class="content">
			<view v-if="showHeader" class="header">
				<!-- 定位城市 -->
				<view class="addr">
					<view class="icon location"></view>
					{{ city }}
				</view>
				<!-- 搜索框 -->
				<view class="input-box">
					<input
						placeholder="默认关键字"
						placeholder-style="color:#c0c0c0;"
						@tap="toSearch()"
					/>
					<view class="icon search"></view>
				</view>
				<!-- 右侧图标按钮 -->
				<view class="icon-btn">
					<view class="icon yuyin-home"></view>
					<view class="icon tongzhi" @tap="toMsg"></view>
				</view>
			</view>
			<uni-search-bar :radius="100" @confirm="search" cancelButton="none"></uni-search-bar>
			<carousel :img-list="imgList" url-key="url" @selected="selectedBanner"/>
		</view>
		<uni-list v-for="(row, index) in tllist" :key="index">
		   <uni-list-item :title="row.name" :note="row.con" :rightText="row.value" to="../detail/detail"></uni-list-item>
		</uni-list>
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
				showHeader:true,
				afterHeaderOpacity: 1,//不透明度
				headerPosition: 'fixed',
				headerTop:null,
				title: 'Hello',
				city: '天津',
				tllist:[{ id: 1, name: '外卖', con: '日结，找一个拿外卖的',value:'¥100' },
					{ id: 2, name: '快递', con: '日结，找一个拿外卖的',value:'¥1900' },
					{ id: 3, name: '家教', con: '日结，找一个拿外卖的',value:'¥100' },
					{ id: 4, name: '零工',  con: '日结，找一个拿外卖的',value:'¥80' },
					{ id: 5, name: '在线',  con: '日结，找一个拿外卖的',value:'¥100' },
					{ id: 6, name: '运动',  con: '日结，找一个拿外卖的',value:'¥100' },
					{ id: 7, name: 'kk',  con: '日结，找一个拿外卖的',value:'¥100' },
					{ id: 8, name: 'aa',  con: '日结，找一个拿外卖的',value:'¥100' }],
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
					},]
			}
		},
		onLoad() {

		},
		methods: {
			selectedBanner(item, index) {
				console.log('', item, index)
			},
			toSearch(){
				uni.navigateTo({
					url:"../search/search"
				})
			}
		}
	}
</script>

<style lang="scss">
	.header {
		width: 92%;
		padding: 0 4%;
		height: 100upx;
		display: flex;
		align-items: center;
		position: fixed;
		top: 0;
		z-index: 10;
		background-color: #fff;
	
		/*  #ifdef  APP-PLUS  */
		top: var(--status-bar-height);
		/*  #endif  */
	
		.addr {
			width: 120upx;
			height: 60upx;
			flex-shrink: 0;
			display: flex;
			align-items: center;
			font-size: 28upx;
			.icon {
				height: 60upx;
				margin-right: 5upx;
				display: flex;
				align-items: center;
				font-size: 42upx;
				color: #ffc50a;
			}
		}
		.input-box {
			width: 100%;
			height: 60upx;
			background-color: #f5f5f5;
			border-radius: 30upx;
			position: relative;
			display: flex;
			align-items: center;
			.icon {
				display: flex;
				align-items: center;
				position: absolute;
				top: 0;
				right: 0;
				width: 60upx;
				height: 60upx;
				font-size: 34upx;
				color: #c0c0c0;
			}
			input {
				padding-left: 28upx;
				height: 28upx;
				font-size: 28upx;
			}
		}
		.icon-btn {
			width: 120upx;
			height: 60upx;
			flex-shrink: 0;
			display: flex;
			.icon {
				width: 60upx;
				height: 60upx;
				display: flex;
				justify-content: flex-end;
				align-items: center;
				font-size: 42upx;
			}
		}
	}
	
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
