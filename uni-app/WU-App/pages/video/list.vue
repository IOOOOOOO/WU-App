<template>
	<view class="page">
		
		<uni-list v-for="(item,index) in list" :key='index'>
			<uni-list-item :title="item.name" @click='tapCell(item.videourl)'></uni-list-item>
			
		</uni-list>
		
		
	</view>	
</template>

<script>
	import uniList from '@/components/uni-list/uni-list.vue'
	import uniListItem from '@/components/uni-list-item/uni-list-item.vue'
	export default{
		components: {uniList,uniListItem},
		data(){
			return {
				list:[]
			}
		},
		onLoad(option) {
			uni.getStorage({
				key:'kechenglist',
				success: (res) => {
// 					var names = []
// 					for (let item of res.data) {
// 						names.push(item.name)
// 					}
					this.list = res.data
				}
			})
		},
		onUnload:function () {
			// 页面卸载的时候清除缓存
			uni.removeStorage({
				key: 'kechenglist',
				success: function (res) {
				}
			});
		},
		methods:{
			tapCell(videourl){
				// console.log(item)
				uni.setStorage({
					key:'videourl',
					data:videourl,
					success: () => {
						uni.navigateTo({
							url:'detail'
						})
					}
				})
			}
		}
		
	}
	
</script>

<style>
	
</style>
