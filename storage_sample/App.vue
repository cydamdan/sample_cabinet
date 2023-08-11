<style lang="scss">

</style>
<script>
	export default {
		// onLaunch: function() {
		// 	console.log('App Launch')
		// },
		// onShow: function() {
		// 	console.log('App Show')
		// },
		// onHide: function() {
		// 	console.log('App Hide')
		// }
		// 获取已过期样品的下标
		getOverDue(){
			let flag = false;
			while(!flag){
				let i = 0;
				let j = 0;
				if(this.categoryList[this.leftId].data[i].info[j].status===2){
					this.overDueOutIndex = i;
					this.overDueInsideIndex = j;
					flag = true;
				}
				console.log(i+'+'+j);
			}
		}
	}
</script>

