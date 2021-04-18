<template>	
	<view class="page">		
		<text class="title">配文偏好可视化</text>					
		<view class="charts-box">
		  <qiun-data-charts
		    type="pie"
		    :chartData="chartData_pie"
		    background="none"
		    :animation="true"
		  />
		</view>
		<u-line color="gray" />
		<!-- 词云图的显示 -->
		<view class="charts-box">
		  <qiun-data-charts
		    type="word"
		    :chartData="chartData_WC"
		    :echartsApp="false"
		    background="none"
		    :animation="true"
		  />
		</view>
		<view>
			<text class="sub_title">根据历史拍照行为生成</text>
		</view>
		<view class="tag_area">			
			<view class="top_scenes">
				<u-button type="primary" size="medium" class="custom-style" style="width: 150rpx;margin: 10px;">常拍景物:</u-button>
				<u-tag shape="circle" :text="tag.name" type="success" style="margin-left: 3px;" v-for="tag in top_scenes"/>
			</view>
			<view class="top_topics">
				<u-button type="success" size="medium" class="custom-style" style="width: 150rpx;margin: 10px;">爱拍主题:</u-button>
				<u-tag shape="circle" :text="tag.name" type="warning" style="margin-left: 3px;" v-for="tag in top_topics"/>
			</view>
			<view class="top_emotions">
				<u-button type="warning" size="medium" class="custom-style" style="width: 150rpx;margin: 10px;">情感偏好:</u-button>
				<u-tag shape="circle" :text="tag.name" type="primary" style="margin-left: 3px;" v-for="tag in top_emotions"/>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				top_scenes:[
					{
						name:"路灯",
					},{
						name:"狗",
					},
					{
						name:"公路"
					}],
				top_topics:[
					{
						name:'夜景',
					},{
						name:'风光人像'	
					},{
						name:'微距'
					},{
						name:'旅游摄影'
					}],
				top_emotions:[
					{
						name:'愉悦'
					},{
						name:'满足'
					}
				],
				chartData:{
				  categories: ["2016", "2017", "2018", "2019", "2020", "2021"],
				  series: [{
				    name: "目标值",
				    data: [35, 36, 31, 33, 13, 34]
				  }, {
				    name: "完成量",
				    data: [18, 27, 21, 24, 6, 28]
				  }]
				},
				chartData_WC:{
				  categories:[],
				  series:[
					   {
						  "name": "马路",
						  "textSize": 25
					   },{
						  "name": "金毛",
						  "textSize": 40
					   },{
						  "name": "樱花",
						  "textSize": 21
					   },{
						  "name": "宠物",
						  "textSize": 14
					   },{
						  "name": "室外",
						  "textSize": 3
					   },{
						  "name": "银杏",
						  "textSize": 15
					   },{
						  "name": "月亮",
						  "textSize": 20
					   },{
						  "name": "夜景",
						  "textSize": 27
					   },{
						  "name": "云",
						  "textSize": 29
					   },{
						  "name": "树叶",
						  "textSize": 22
					   },{
						  "name": "汽车",
						  "textSize": 21
					   },{
						  "name": "湖边",
						  "textSize": 9
					   },{
						  "name": "花朵",
						  "textSize": 13
					   },
				  ],
				},
				chartData_pie:{
					categories:[],
					series:[{
						"data":[
							{
							  "name": "马路",
							  "value": 25
							},{
							  "name": "金毛",
							  "value": 40
							},{
							  "name": "樱花",
							  "value": 21
							},{
							  "name": "宠物",
							  "value": 14
							},{
							  "name": "室外",
							  "value": 3
							},{
							  "name": "银杏",
							  "value": 15
							},{
							  "name": "月亮",
							  "value": 20
							},{
							  "name": "夜景",
							  "value": 27
							},{
							  "name": "汽车",
						      "value": 21
							},{
							  "name": "湖边",
						      "value": 9
							},{
							  "name": "花朵",
						      "value": 13
							},
						]
					}]
				},
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.page{
	display: flex;
	flex-direction: column;
	width: 100%;
	height: 100%;
}
.title {
			font-size: 18px;
			font-weight: 500;
			color: rgba(43, 43, 43, 1);
			line-height: 41px;
			width: 100%;
			display: flex;
			align-items: center;
			justify-content: center;
		}
.charts-box{
	width: 100%;
	height: 500rpx;
}
.sub_title {	
	margin-left: 10px;
	font-size: 14px;
	font-weight: 90%;				
	line-height: 40px;
			}
.tag_area{
	display: flex;
	flex-direction: column;
	justify-content: flex-start;
	height: 400upx;
	width: 90%;
	margin-left:5%;
	margin-right:5%;
}
.top_scenes{
	display: flex;
	flex-direction: row;
	justify-content: flex-start;
	align-items: center;
}
</style>
