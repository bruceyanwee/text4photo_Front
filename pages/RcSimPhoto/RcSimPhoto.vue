<template>
	<view class="page">
		<view class="header">			
			<text class="title">仿拍优秀作品</text>			
		</view>
		<u-line color="gray"></u-line>
		<view class="title_line">
			<text class="title">你的作品</text>			
		</view>
		<u-image width="100%" height="500rpx" :src="my_src" border-radius="10px"></u-image>
		<view style="display: flex;flex-direction: row;justify-content: space-around;">
			<u-button @click="onGetImgClick" type="success" style="margin: 5px;">拍照或上传</u-button>
			<u-button @click="search_sim" type="success" style="margin: 5px;">仿拍推荐</u-button>
		</view>		
		<view class="title_line">
			<text class="title">推荐依据</text>
		</view>
		<view class="recommd_reason_block">			
			<u-tag :text="kw" type="success" shape="circle" style="margin-left: 15px;" v-for="kw in reason_kws"></u-tag>
		</view>					
		<scroll-view scroll-x="true" class="scroll_item" style="margin-top: 10px;">
			<view class="single_poster" v-for="itemObject in recommd_items" :key="itemObject.id">
				<view class="poster-wapper">
					<u-image width="100%" border-radius="10px" height="400upx" :src="itemObject.img_url"></u-image>
					<u-button type="primary" shape="circle" style="margin: 5px;"size="medium">点我仿拍</u-button>	
					<view >
						<text style="font-size: 10px; color:gray;">推荐依据</text>
						<u-tag style="margin-left: 5px;" shape="circle" mode="light" type="success" :text="itemObject.kw"></u-tag>
					</view>
					
				</view>
			</view>									
		</scroll-view>		
	</view>
</template>

<script>
	const recmd_items_data = require('@/common/json/recmd_items_sim.json');
	export default {		
		data() {
			return {
				my_src:'https://images.unsplash.com/photo-1557456170-0cf4f4d0d362?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8bGFrZXxlbnwwfHwwfHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60',
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
			search_sim:function(){
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

</style>

<style lang="scss" scoped>
	@function realSize($args) {
		@return $args / 1.5;
	}
.page{
	width: 100%;
	height: 100%;
	background-color:#f7f7f7;
	
}
.page-block {
	background-color: #FFFFFF;
}	
.recommd_reason_block{
	display: flex;
	flex-direction: row;	
	justify-content: flex-start;
}
.single_poster{
	display: inline-block;
	margin: 10px;
}
.scroll_item{
	width: 100%;
	white-space: nowrap;
}
.poster-wapper{
	display: flex;
	flex-direction: column;
}
.poster{
	width: 500upx;
	height: 300upx;
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
