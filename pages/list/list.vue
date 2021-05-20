<template>
	<view class="">
		<uni-list v-for="(row, index) in tllist" :key="index">
		    <uni-list-item :title="row.name" :note="row.con" :rightText="row.value" to="../detail/detail"></uni-list-item>
		</uni-list>
  </view>
	
</template>

<script>
	export default{
		data(){
			return{
				tllist:[{ id: 1, name: '外卖', con: '日结，找一个拿外卖的',value:'¥100' },
					{ id: 2, name: '快递', con: '日结，找一个拿外卖的',value:'¥1900' },
					{ id: 3, name: '家教', con: '日结，找一个拿外卖的',value:'¥100' },
					{ id: 4, name: '零工',  con: '日结，找一个拿外卖的',value:'¥80' },
					{ id: 5, name: '在线',  con: '日结，找一个拿外卖的',value:'¥100' },
					{ id: 6, name: '运动',  con: '日结，找一个拿外卖的',value:'¥100' },
					{ id: 7, name: 'kk',  con: '日结，找一个拿外卖的',value:'¥100' },
					{ id: 8, name: 'aa',  con: '日结，找一个拿外卖的',value:'¥100' }],
			}
		}
	}
</script>

<style>
</style>
