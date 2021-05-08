<template>
	<view class="page">		
		<text class="title">用户情感偏好可视化</text>					
		<!-- 情感雷达图的显示 -->
		<view class="charts-box">
		  <qiun-data-charts
		    type="radar"
		    :chartData="chartData_radar"
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
				<u-button type="primary" size="medium" class="custom-style" style="width: 150rpx;margin: 10px;">照片情感:</u-button>
				<u-tag shape="circle" :text="tag.name" type="success" style="margin-left: 3px;" v-for="tag in top_scenes"/>
			</view>
			<view class="top_topics">
				<u-button type="success" size="medium" class="custom-style" style="width: 150rpx;margin: 10px;">配文情感:</u-button>
				<u-tag shape="circle" :text="tag.name" type="warning" style="margin-left: 3px;" v-for="tag in top_topics"/>
			</view>
			<view class="top_emotions">
				<u-button type="warning" size="medium" class="custom-style" style="width: 150rpx;margin: 10px;">多模态情感:</u-button>
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
						name:"愉快",
					},{
						name:"敬畏",
					},
					{
						name:"有趣"
					}],
				top_topics:[
					{
						name:'满足',
					},{
						name:'悲伤'	
					}],
				top_emotions:[
					{
						name:'愉悦'
					},{
						name:'满足'
					}
				],
				chartData_radar:{
					"categories": [
						"有趣",
						"敬畏",
						"愉快",
						"满足",
						"愤怒",
						"恶心",
						"恐怖",
						"悲伤",
					],
					"series": [
						{
							"name": "图像情感",
							"data": [
								90,
								110,
								165,
								195,
								187,
								172,
								122,
								143,
							]
						},
						{
							"name": "文本情感",
							"data": [
								190,
								210,
								105,
								35,
								27,
								102,
								132,
								91,
							]
						},
						{
							"name": "多模态情感",
							"data": [
								150,
								165,
								125,
								165,
								87,
								122,
								112,
								120,
							]
						}
					]
				},
				chartData_WC:{
				  categories:[],
				  series:[
					   {
						  "name": "有趣",
						  "textSize": 25
					   },{
						  "name": "悲伤",
						  "textSize": 40
					   },{
						  "name": "敬畏",
						  "textSize": 21
					   },{
						  "name": "恐怖",
						  "textSize": 9
					   },{
						  "name": "愉快",
						  "textSize": 13
					   },{
						  "name": "满足",
						  "textSize": 29
					   }					   
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
