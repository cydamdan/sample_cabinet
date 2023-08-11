<template>
	<view class="content">
		<view class="mui-content-padded">
			<!-- 列表组件 -->
			<cc-listView :sampleList="sampleList" @click="goProDetail"></cc-listView>
		</view>
		<!--  totalNum: 条目总数量  pageCount:设置分页数量  curPageNum:设置当前页-->
		<cc-listPageView :totalNum="totalNum" :pageCount="pageCount" :curPageNum="curPageNum" @pageClick="pageClick">
		</cc-listPageView>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				totalNum: 0,
				pageCount: 10,
				curPageNum: 1,
				// 列表数组
				sampleList: []
			}
		},
		onLoad() {
			// 请求数据
			this.requestData();
		},
		methods: {
			// 列表条目点击事件
			goProDetail(item) {},
			// 分页事件
			pageClick(tag) {
				if (tag === 0) {
					// 上一页 (不等于第一页)
					if (this.curPageNum > 1) {
						this.curPageNum--;
						this.requestData();
					}
				} else {
					// 下一页 (不等于最后一页)
					if (this.totalNum > (this.curPageNum * 10)) {
						this.curPageNum++;
						this.requestData();
					}
				}
			},
			// 请求数据
			requestData() {
				// 订单编号为当天日期+id
				let today = new Date();
				let year = today.getFullYear();
				let month = today.getMonth() + 1;
				let day = today.getDate();
				if (month < 10) {
				  month = "0" + month;
				}
				if (day < 10) {
				  day = "0" + day;
				}
				let date = year + "" + month + "" + day;
				// 模拟请求参数设置
				let reqData = {
					'area': '',
					"pageSize": 10,
					"pageNo": this.curPageNum
				}
				// 模拟请求接口
				this.totalNum = 39;
				this.sampleList = [];
				for (let i = 0; i < 10; i++) {
					this.sampleList.push({
						'id': i + '',
						'sampleName': '样品名称' + i,
						'sampleNumber': '订单编号' + date + i,
						'area': '所属食堂',
						'sampleTime': '留样时长',
						'stage': '样品状态',
						'imgurl': 'https://cdn.uviewui.com/uview/album/3.jpg'
					});
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	page {
		background-color: #f7f7f7;
	}

	.content {
		display: flex;
		flex-direction: column;
	}

	.mui-content-padded {
		margin: 0px 14px;
		/* background-color: #ffffff; */
	}
</style>