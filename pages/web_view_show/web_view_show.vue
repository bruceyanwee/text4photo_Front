<!-- 可用第三方平台
https://500px.com.cn/ 
https://fotomen.cn/2015/04/07/sakurajiang/
https://www.pexels.com/
https://unsplash.com/
-->
<!-- 教程类
http://www.fsbus.com/
http://letsfilm.org/
https://www.zhihu.com/question/287110029/answer/454879816
 -->
<template>
    <view class="app">
		<view>
			this is a view
		</view>
        <web-view :src="src">this is a web-view</web-view>
    </view>
</template>

<script>
    export default {

        data() {
            return {
                src: ''
            }
        },
        //接收传递的参数
        onload(option) {
			debugger;
			this.src = option.url;
			console.log(this.src);          
        },
		onReady(option) {
			// debugger;
			this.src = option.url;
			console.log(this.src);
		},
		onShow(option) {
			// debugger;
			this.src = option.url;
			console.log(this.src);
		},
        methods: {

        }
    }
</script>
