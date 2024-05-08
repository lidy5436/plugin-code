<template>
	<view>
		<lidy-sideslip>
			<lidy-sideslip-item ref="lidySideslipItemRef" v-for="(item,index) in list" :data="item" :key="index"
				:options="options" @OptionsSideslipClick="handleOption">
				<view class="card">{{item}}</view>
			</lidy-sideslip-item>
		</lidy-sideslip>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [
					'第一条数据',
					'第二条数据',
					'第三条数据',
					'第四条数据',
					'第五条数据',
					'第六条数据',
				],
				options: [{
						title: '关注',
						code: 'follow',
						background: '#FBC21C'
					},
					{
						title: '删除',
						code: 'del',
						background: '#FF0000'
					}
				]
			}
		},
		onLoad() {

		},
		methods: {
			handleOption(code, item) {
				switch (code) {
					case 'follow':
						console.log("点击了【关注】,提交了数据:" + item)
						break
					case 'del':
						console.log("点击了【删除】,提交了数据:" + item)
						break
					default:
						break
				}
				this.closeSideslipItem()
			},
			/**
			 * 关闭所有子标签
			 */
			closeSideslipItem() {
				const size = this.$refs.lidySideslipItemRef.length
				for (let i = 0; i < size; i++) {
					this.$refs.lidySideslipItemRef[i].resetTouch()
				}
			}
		}
	}
</script>

<style>
	.card {
		height: 45px;
		display: flex;
		align-items: center;
		padding-left: 12px;
	}
</style>