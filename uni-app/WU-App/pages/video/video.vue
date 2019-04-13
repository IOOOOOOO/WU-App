<template>
	<view class="page">
		
		<page-head :title="title"></page-head>
		<view class="uni-product-list">
			<view class="uni-product" v-for="(product,index) in productList" :key="index">
				<view class="image-view">
					<image @click="imgClick(index)" v-if="renderImage" class="uni-product-image" :src="product.image"></image>
				</view>
				<view class="uni-product-title">{{product.title}}</view>
				
			</view>
		</view>
	</view>
</template>

<script>
	import common from '../../common/common.js'
export default {
    data() {
        return {
            title: 'product-list',
			productList: [],
            renderImage: false,
			
        };
    },
	onUnload(){
		
	},
	onLoad() {
		
	    this.loadData();
	    setTimeout(()=> {
	        this.renderImage = true;
	    }, 300);
	},
	onPullDownRefresh() {
// 	    this.loadData('refresh');
// 	    // 实际开发中通常是网络请求，加载完数据后就停止。这里仅做演示，加延迟为了体现出效果。
// 	    setTimeout(() => {
// 	        uni.stopPullDownRefresh();
// 	    }, 2000);
	},
	onReachBottom() {
	    this.loadData();
	},
    methods: {
		imgClick:function(index){
			// console.log('图片被点击了' + this.productList[index].kecheng)
			uni.setStorage({
				key:'kechenglist',
				data:this.productList[index].kecheng,
				success: () => {
					uni.navigateTo({
						url:'list'
					})
				}
			})
		},
		
        loadData(action = 'add') {
			// var datajson = require('./common/data.json');
			uni.showLoading({
				title: '加载中',
				mask: false
			});
			uni.request({
				url:common.domain + '/videos',
				success: (res) => {
					// console.log(res.data);
					this.productList = res.data['data'];
					uni.hideLoading()
				}
			})
            // const data = datajson.list;

//             if (action === 'refresh') {
//                 this.productList = [];
//             }
// 
//             data.forEach(item => {
//                 this.productList.push(item);
//             });
        }
    },
    
};
</script>

<style>
	@import url("/common/video.css");
</style>
