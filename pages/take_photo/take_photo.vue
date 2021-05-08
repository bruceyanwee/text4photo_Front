<template>
	<view class="page-all">
		<view class="title-h1">
			<text style="width:fit-content;">开始拍照</text>
			<image src="../../static/paizhao.png" class="title-img"></image>
		</view>
		<view class="start-area">
			<view >
				<image :src="photo_local_url" mode="aspectFit" class="photo-area" border-radius="10px"></image>
				<!-- <u-image :src="photo_local_url" mode="aspectFit" class="photo-area" border-radius="5px"></u-image> -->
			</view>
			<view class="two-btn">
				<button type="primary" style="background-color:#DD524D;font-size: 10px;" @click="onGetImgClick()">点击拍照</button>
				<button type="primary" style="color: #FFFFFF;background-color: #F0AD4E;font-size: 10px" @click="onRecognize">点击识别</button>
			</view>
		</view>
		<view>			
			<textarea value="" placeholder="输入你此刻的心情(比如:现在想一个人静静)" class="user-text" auto-height="true"/>
		</view>
		<view class="title-h1" style="display: flex;flex-direction: row;">
			<text style="width:fit-content;">识别结果</text><image src="../../static/baogao.png" class="title-img"></image>
		</view>
		<!-- 识别结果展示区 -->	
		<view class="title-h2">情感分布</view>
		<view class="charts-box">
		  <qiun-data-charts
			type="radar"
			:chartData="chartData_RD"
			background="none"
			:animation="true"
		  />
		</view>
		<view class="title-h2">场景属性</view>
		<view class="charts-box">
		  <qiun-data-charts
		    type="word"
		    :chartData="chartData_WC"
		    background="none"
		    :animation="true"
		  />
		</view>	
		<view class="title-h2">场景类别</view>
		<view class="charts-box">
		  <qiun-data-charts
		    type="ring"
		    :chartData="chartData_SC"
		    background="none"
		    :animation="true"
		  />		
		</view>		
		<view class="title-h1" style="display: flex;flex-direction: row;">
			<text style="width:fit-content;">试试下面的配文</text>
			<image src="../../static/peiwen.png" class="title-img"></image>			
		</view>
		<view class="start-area">			
			<textarea value="" placeholder="推荐文案展示区" class="peiwen-area" />			
			<view class="two-btn">
				<button type="primary" style="background-color:#DD524D;font-size: 10px">换一条</button>
				<button type="primary" style="color: #FFFFFF;background-color: #F0AD4E;font-size: 10px">使用此文案</button>
			</view>
		</view>		
	</view>	
</template>

<script>
	export default {
		data() {
			return {								
				photo_local_url:'',
				chartData_RD:{
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
							"name": "情感概率分布",
							"data": [
								0,
								0,
								0,
								0,
								0,
								0,
								0,
								0,
							]
						}
					]
				},
				chartData_WC:{
				  categories:[],
				  series:[{
					  "name":"上传识别才有结果哦",
					  "textSize":20
				  }],
				},
				chartData_SC:{
				  categories:[],
				  series:[
					  {
						  "data":[]
					  }
				  ],
				},
			}
		},
		methods: {
			onGetImgClick:function() {
				const that = this;
				uni.chooseImage({
					count: 1, // 最多可以选择的图片张数，默认9
					sizeType: ['original', 'compressed'], //original 原图，compressed 压缩图，默认二者都有
					sourceType: ['album', 'camera'], //album 从相册选图，camera 使用相机，默认二者都有。如需直接开相机或直接选相册，请只使用一个选项
					success: function (res) {
						console.log('预览图片成功');
						console.log(JSON.stringify(res.tempFilePaths));
						that.photo_local_url = res.tempFilePaths[0]
					}
				});
			},
			onRecognize:function(){
				const that = this;
				uni.uploadFile({
				            url: 'http://127.0.0.1:8080/take_photo', //仅为示例，非真实的接口地址
							// url: 'http://106.13.225.94:8080/take_photo', //仅为示例，非真实的接口地址
				            filePath: that.photo_local_url,							
				            name: 'file',
				            formData: {
				                'user': 'test'
				            },
				            success: (uploadFileRes) => {
								console.log('上传照片成功');
								console.log(uploadFileRes.statusCode);
								// 处理识别的结果，填到识别结果展示区，包括：情感类别以及概率分布，照片内容，配文展示																
								var rst = JSON.parse(uploadFileRes.data);
								var radar_arr = rst.sentiment;	
								var sc_arrts = rst.scene_results.scene_attributes;
								var sc_catgs = rst.scene_results.scene_category;
								that.chartData_RD['series'][0]['data'] = radar_arr;	
								that.chartData_WC['series'] = sc_arrts;
								that.chartData_SC['series'][0]['data'] = sc_catgs;
				            }
				        });
			}
			
		}
	}
</script>

<style>
.page-all{
	width: 100%;
	height: 100%;
	margin: 0rpx;
	padding: 0rpx;
	position: absolute;
}
.title-h1{
	display: flex;
	flex-direction: row;
	width: 100%;
	margin-top: 20px;
	padding-left:12px;
	font-weight: bold;
	font-size: 20px;
	font-style: italic;
	height: 30px;
}
.title-img{
	width: 25px;
	height: 25px;
	padding-left: 10px;
}
.title-h2{
	width: 100%;
	margin-top: 20px;
	padding-left:20px;
	font-weight: bold;
	font-size: 17px;
	font-style: italic;
}
.start-area{
	width: 100%;
	background-color: #FFFFFF;
	padding-left: 20px;	
	display: flex;
	flex-direction: row;
}
.photo-area{
	width: 500upx;
	height: 600upx;	
}
.inner-img{
	width:fit-content;
	border-radius: 16px;
}
.two-btn{
	display: flex;
	flex-direction:column ;
	justify-content: space-around;
	padding-left: 15upx;
}
.user-text{
	padding-left: 20px;
	font-size: 15px;
	width: 100%;
}
.result-area{
	display: flex;
	flex-direction: column;
}
.peiwen-area{
	width: 500rpx;
	height: 300rpx;
	margin-top: 20px;
	font-size: 15px;
}

.charts-box{
	width: 100%;
	height: 400rpx;
}
</style>
