<template>
	<view class="page">
		<view class="header">			
			<text class="title">摄影理论推荐</text>			
		</view>
		<u-line color="gray"></u-line>
		<view class="title_line">
			<text class="title">你的作品</text>			
		</view>
		<u-image width="100%" height="500rpx" :src="my_src" border-radius="10px"></u-image>
		<view style="display: flex;flex-direction: row;justify-content: space-around;">
			<u-button @click="onGetImgClick" type="success" style="margin: 5px;">拍照或上传</u-button>
			<u-button @click="click_recommd" type="success" style="margin: 5px;">点击推荐</u-button>
		</view>		
		<view class="title_line">
			<text class="title">推荐依据</text>
		</view>
		<view class="recommd_reason_block">			
			<u-tag :text="kw" type="success" shape="circle" style="margin-left: 15px;" v-for="kw in reason_kws"></u-tag>
		</view>			
		<!-- 摄影教程卡片展示区 -->
		<view class="recom_area">
			<view class="simgle-item" v-for="itemObject in recommd_items">					
				<image mode="aspectFit" 
					   :src="itemObject.img_url"
					   style="width: 375rpx;height: 200rpx;flex-shrink: 0;border-radius: 8px;"					   >
				</image>															
				<view class="rcm-item-desc">
					<view class="rcm-title">
						{{itemObject.title}}
					</view>
					<view class="rcm-info">
						<text style="color: gray;">来自</text>
						<text style="color: #2C405A;margin-left: 5px;"> {{itemObject.res_from}}</text>
					</view>	
					<view class="rcm-info">
						<text style="color: gray;">推荐依据</text>
						<u-tag :text="itemObject.kw" type="success" shape="circle" style="margin-left: 15px;"></u-tag>
					</view>	
														
				</view>
			</view>
		</view>		
		
	</view>
</template>

<script>
	const recmd_items_data = require('@/common/json/recmd_items_theory.json');
	export default {		
		data() {
			return {
				my_src:'http://letsfilm.org/wp-content/uploads/2020/12/morgan-sessions-YIN4xUBaqnk-unsplash.jpg',
				reason_kws : [],
				recommd_items:[],
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
						that.my_src = res.tempFilePaths[0];
					}
				});
			},
			// 暂时用到的json模拟的数据
			click_recommd:function(){
				const show_num = 3;
				this.recommd_items = recmd_items_data.item_List.sort(function(){
					return 0.5-Math.random();					
				}).slice(0,show_num);	
				this.reason_kws = recmd_items_data.recomd_reason_kws.sort(function(){
					return 0.5-Math.random();					
				}).slice(0,show_num);	
			}
	},
	}
</script>

<style>
/* 推荐 教程部分的样式 */
.page{
	width: 750upx;
	height: 100%;
	background-color:#f7f7f7;
	
}
.recom_area{
	width: 100%;
	height: 100%;
	display: flex;
	flex-direction: column;		
	
	}
.simgle-item{				
		display: flex;
		flex-direction: row;						
		height: 300rpx;
		width: 100%;
		align-items: center;
		justify-content:flex-start;
	}
.rcm-item-desc{
	width: 375rpx;
	height: 80%;
	display: flex;
	margin: 5px;
	flex-direction: column;
	justify-content:space-around;
	align-items: flex-start;
}
.rcm-title{
	width: 100%;
	font-size: 18px;
	margin-bottom: 30rpx;	
	white-space: nowrap;
	text-overflow:ellipsis;
	overflow: hidden;	
	
}
</style>

<style lang="scss" scoped>
	@function realSize($args) {
		@return $args / 1.5;
	}

.page-block {
	background-color: #FFFFFF;
}	
.recommd_reason_block{
	display: flex;
	flex-direction: row;	
	justify-content: flex-start;
	height: 100%;
}
.single_poster{
	display: inline-block;
	margin: 10px;
}
.poster{
	width: 100%;
	height: 100%;
}
.game-name{
	width: 200upx;
	margin-top: 10upx;
	font-size: 15px;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}

.page_content {
	width: 100%;
	display: flex;
	flex-direction: column;
	align-items: center;
}

.header {		
		width: 95%;
		display: flex;
		flex-direction: row;
		align-items: center;
		margin-left: 10px;
		margin-right: 10px;

		.btn {
			width: 27px;
			height: 27px;
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
	}

	.logo {
		margin-top: 10px;
		width: 100px;
		height: 100px;
	}
	.title_line {
		width: 100%;
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;
	
		.title {
			margin-left: 20px;
			font-size: 18px;
			font-weight: 500;
			color: rgba(51, 51, 51, 1);
			line-height: 41px;
		}
	}
</style>
