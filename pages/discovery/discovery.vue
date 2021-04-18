<template>
	<view class="app">					
		<u-tabs :list="tab_list" :is-scroll="false" :current="current" @change="change"></u-tabs>
		<waterfall-flow :list="list" @click="choose"></waterfall-flow>
	</view>
</template>

<script>
	// 瀑布流组件
	import WaterfallFlow from '@/components/nairenk-waterfall-flow/nairenk-waterfall-flow.vue';
	// 模拟 JSON 数据
	const data = require('@/common/json/data.json');
	export default {
		components: {
			WaterfallFlow
		},
		data() {
			return {
				tab_list:[
					{
						name:"关注"
					},{
						name:"发现"
					},{
						name:"附近"
					}],
				current:0,
				keyword:'人像',
				page: 1,
				start: 0,
				end: 0,
				list: [], // 列表
			}
		},
		onLoad() {
			this.getList();
		},
		onReachBottom() {
			this.page++;
			this.getList();
		},
		onPullDownRefresh(){
			console.log('refresh');
			// this.random_once();
			setTimeout(function () {
				uni.stopPullDownRefresh();
			}, 1000);
		},		
		methods: {
			change(index) {
					this.current = index;
				},
			random_once(){										
				data.list.sort(function(){
					return 0.5-Math.random();					
				});
				this.page = 1;
				this.start =0;
				this.end = 0;
				this.list = []; 
				this.getList();
			},
			// 选中
			choose(item) {
				// item 返回选中 JSON 对象
				console.log(item)
			},
			// 模拟加载数据
			getList() {				
				if (this.list.length < data.list.length) {
					uni.showLoading({
						title: '加载中...'
					})
					setTimeout(() => {
						this.end = this.page * 10;
						this.list = this.list.concat(data.list.slice(this.start, this.end));
						this.start = this.end;
						uni.hideLoading();
					}, 1000)
				}
			}
		}
	}
</script>

<style>
</style>
