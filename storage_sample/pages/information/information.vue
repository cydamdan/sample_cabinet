<template>
	<view class="container">
		<uni-section title="留样信息" type="line">
			<view class="form">
				<uni-forms ref="baseForm" :rules="rules" :model="baseFormData" labelWidth="80px">
					<uni-forms-item label="样品名称" name="name" required>
						<uni-easyinput type="text" v-model="baseFormData.name" placeholder="请输入样品名称" />
					</uni-forms-item>
					<uni-forms-item label="样品来源" name="source" required>
						<uni-easyinput type="text" v-model="baseFormData.source" placeholder="请输入来源" />
					</uni-forms-item>
					<uni-forms-item label="留样时长" required>
						<uni-data-select v-model="baseFormData.time" :localdata="timeRange">
						</uni-data-select>
					</uni-forms-item>
					<uni-forms-item label="样品描述">
						<uni-easyinput type="textarea" v-model="baseFormData.introduction" placeholder="请输入样品描述" />
					</uni-forms-item>
					<uni-forms-item label="样品照片" name="photos" required>
						<view class="example-body">
							<uni-file-picker limit="3" fileMediatype="image" title="最多选择3张图片" :source-type="sourceType"
								v-model="baseFormData.photos" @progress="progress" @success="success" @fail="fail"
								@select="select"></uni-file-picker>
						</view>
					</uni-forms-item>
				</uni-forms>
				<button type="default" @click="submit">提交</button>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 照片可选择模式
				sourceType: ['album', 'camera'],
				imageValue: [],
				imgUrl: '',
				// 基础表单数据
				baseFormData: {
					name: '',
					source: '',
					introduction: '',
					time: 0,
					photos: []
				},
				// 留样时长选择范围
				timeRange: [{
						value: 0,
						text: "24小时"
					},
					{
						value: 1,
						text: "48小时"
					},
					{
						value: 2,
						text: "72小时"
					},
				],
				// 校验规则
				rules: {
					// 样品名称校验
					name: {
						rules: [{
							required: true,
							errorMessage: '请输入样品名称'
						}]
					},
					// 样品来源校验
					source: {
						rules: [{
							required: true,
							errorMessage: '请输入样品来源'
						}]
					},
					photos: {
						rules: [{
							required: true,
							errorMessage: '请选择样品图片'
						}]
					}
				},
			}
		},
		onLoad() {},
		// onReady() {
		// 	// 设置自定义表单校验规则，必须在节点渲染完毕后执行
		// 	this.$refs.customForm.setRules(this.customRules)
		// },
		methods: {
			// 获取上传状态
			select(e) {
				// console.log('选择文件：', e);
				let dataObj = e;
				this.baseFormData.photos.push(dataObj);
				console.log('要添加的数据是：',dataObj);
			},
			// 删除图片
			deletePic(event) {
				this[`fileList${event.name}`].splice(event.index, 1)
			},
			// 获取上传进度
			progress(e) {
				console.log('上传进度：', e)
			},

			// 上传成功
			success(e) {
				console.log('上传成功');
				const path = JSON.parse(res.data);
				// 后端返回的地址，存入图片地址
				this.baseFormData.photos.push(path.imgUrl);
				console.log('baseFormData.photos',this.baseFormData.photos);
				// this.$refs.baseForm.setValue('photos',this.baseFormData.photos);
				// this.baseFormData.photos = JSON.parse(res.data).data;
				// console.log(this.baseFormData.photos);
			},
			// 上传失败
			fail(e) {
				console.log('上传失败：', e)
			},
			onClickItem(e) {
				console.log(e);
				this.current = e.currentIndex
			},
			del(id) {
				let index = this.dynamicLists.findIndex(v => v.id === id)
				this.dynamicLists.splice(index, 1)
			},
			submit() {
				// console.log(this.baseFormData);
				this.$refs.baseForm.validate().then(res => {
					console.log('success', res);
					uni.showToast({
						title: `校验通过`,
					})
					console.log(res.data);
				}).catch(err => {
					console.log('err', err);
				})
			},
		}
	}
</script>

<style lang="scss">
	.form {
		padding: 15px;
		background-color: #fff;
	}

	.segmented-control {
		margin-bottom: 15px;
	}

	.button-group {
		margin-top: 15px;
		display: flex;
		justify-content: space-around;
	}

	.form-item {
		display: flex;
		align-items: center;
		flex: 1;
	}

	.button {
		display: flex;
		align-items: center;
		height: 35px;
		line-height: 35px;
		margin-left: 10px;
	}
</style>