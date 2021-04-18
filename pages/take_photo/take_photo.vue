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
		<view class="result-area">
			<view class="result-emtion title-h2">
				情感: <text v-for="s in senti_words" style="font-size: 10px;padding-left: 4px;">
					 {{s.class}} ({{s.proba}})、
					</text>
			</view>
			<view class="result-emtion title-h2">
				内容:<text v-for="s in content_words" style="font-size: 10px;padding-left: 4px;">
					 {{s.class}} ({{s.proba}})、
					</text>
			</view>
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
				senti_words:[
					{
						class:'悲伤',
						proba:0.12
					},
					{
						class:'失落',
						proba:0.59
					},
					{
						class:'高兴',
						proba:0.34
					},
				],
				content_words:[
					{
						class:'房屋',
						proba:0.12
					},
					{
						class:'室外',
						proba:0.59
					},
					{
						class:'河流',
						proba:0.34
					},
				],
				photo_local_url:'',				
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
						that.photo_local_url = res.tempFilePaths[0]
					}
				});
			},
			onRecognize:function(){
				const that = this;
				uni.uploadFile({
				            url: 'http://106.13.225.94:5000/test', //仅为示例，非真实的接口地址
				            filePath: that.photo_local_url,							
				            name: 'file',
				            formData: {
				                'user': 'test'
				            },
				            success: (uploadFileRes) => {
								console.log(uploadFileRes.statusCode);
				                console.log(uploadFileRes.data);
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
</style>
