<template>
	<view>
		<uv-toast ref="toast"></uv-toast>
		<wm-list-add ref="add" @clickAdd="clickAdd" />
		<!-- category-list：分类列表  @itemClick：条目点击 -->
		<cc-beautyCate :category-list="categoryList" @showCategoryIndex="selectLeftOn" @itemClick="toCategory"></cc-beautyCate>
	</view>
</template>
<script>
	import {
		Static
	} from "vue"
	// 导入侧边添加组件
	import wmListAdd from '@/components/wm-list-add/wm-list-add';
	export default {
		components: {
			wmListAdd
		},
		data() {
			return {
				leftId : 0,
				// overDueOutIndex: 0,
				// overDueInsideIndex: 0,
				categoryList: [{
						cid: 0,
						main_name: '1号食堂',
						data: [{
								next_name: '素菜',
								info: [{
										son_name: '生菜',
										imgurl: "../../static/square_fill.png",
										status: 1
									},
									{
										son_name: '卷心菜',
										imgurl: "../../static/square_fill.png",
										status: 1
									},
									{
										son_name: '茄子',
										imgurl: "../../static/square_fill.png",
										status: 1
									},
									{
										son_name: '玉米',
										imgurl: "../../static/square_fill.png",
										status: 1
									},
									{
										son_name: '土豆',
										imgurl: "../../static/square.png",
										status: 0
									},
								],
							},
							{
								next_name: '肉类',
								info: [{
										son_name: '牛肉',
										imgurl: "../../static/square_fill.png",
										status: 1
									},
									{
										son_name: '鱼',
										imgurl: "../../static/square.png",
										status: 0
									},
									{
										son_name: '鸡肉',
										imgurl: "../../static/square_error.png",
										status: 2
									}
								]
							}
						]
					},
					{
						cid: 1,
						main_name: '2号食堂',
						data: [{
								next_name: '素菜',
								info: [{
										son_name: '玉米',
										imgurl: "../../static/square_error.png",
										status: 2
									},
									{
										son_name: '土豆',
										imgurl: "../../static/square_fill.png",
										status: 1
									},
								],
							},
							{
								next_name: '肉类',
								info: [{
									son_name: '鱼',
									imgurl: "../../static/square_fill.png",
									status: 1
								}]
							}
						]
					},
					{
						cid: 2,
						main_name: '3号食堂',
						data: [{
								next_name: '素菜',
								info: [{}]
							},
							{
								next_name: '肉类',
								info: [{}]
							}
						]
					},
					{
						cid: 3,
						main_name: '6号食堂',
						data: [{
								next_name: '素菜',
								info: [{}]
							},
							{
								next_name: '肉类',
								info: [{}]
							}
						]
					},
					{
						cid: 4,
						main_name: '10号食堂',
						data: [{
								next_name: '素菜',
								info: [{}]
							},
							{
								next_name: '肉类',
								info: [{}]
							}
						]
					}
				]
			}
		},
		methods: { 
			// 组件源文件中的showCategory(idnex)函数
			selectLeftOn(index){
				// index=左侧导航栏选中的cid
				this.leftId = index;
			},
			// 检测是否过期
			checkOverdue(){
			},
			clickAdd() {
				// 左侧导航栏由cid决定
				let addData = {son_name:'未命名',imgurl:'../../static/square.png',status:0};
				let index = this.leftId;
				let vegetable = this.categoryList[index].data[0];
				let meat = this.categoryList[index].data[1];
				uni.showActionSheet({
					itemList: ['添加素菜留样柜', '添加肉类留样柜'],
					success: function (res) {
						if(res.tapIndex===0){
							console.log('选中了第' + (res.tapIndex + 1) + '个按钮');
							vegetable.info.push(addData);
							
						}else{
							console.log('选中了第' + (res.tapIndex + 1) + '个按钮');
							meat.info.push(addData);
						}
					},
					fail: function (res) {
						// console.log(res.errMsg);
					}
				});
			},
			// 分类条目点击
			toCategory(item,index) {}
		}
	}
</script>
<style lang="scss">

</style>