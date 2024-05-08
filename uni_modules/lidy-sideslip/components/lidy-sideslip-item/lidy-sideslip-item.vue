<template>
	<view class="container-wrapper" :style="{
		width: `calc(100% + ${optionWidth}px)`,
		marginLeft: `-${optionWidth}px`,
		transform: isTouchMove?`translateX(0px)`:`translateX(${optionWidth}px)`
	}">
		<view class="container" @touchstart="touchstart" @touchend="touchend">
			<slot></slot>
		</view>
		<view class="options-wrapper">
			<view class="option-title" v-for="(option,index) in options" :key="index"
				:style="{backgroundColor: `${option.background}`}" @click="handleOptions(option.code)">
				{{option.title}}
			</view>
		</view>
	</view>
</template>

<script>
	/**
	 * 侧滑操作子组件
	 * @description 侧滑操作子组件，用于存放侧滑的明细条目数据
	 * @property {Object} 	data  		明细条数据，必填
	 * @property {Array} 	options		自定义操作列
	 * 	@value {String}		title		操作栏标题,必填
	 * 	@value {String}		code		唯一编码,必填,唯一
	 * 	@value {String}		background	操作栏颜色
	 * @event {Function}	OptionsSideslipClick(code,data) 	侧边栏点击事件
	 * 	@value {String}		code		按钮唯一编码
	 * 	@vlaue {Object}		data		明细数据
	 * 
	 */
	export default {
		name: 'lidy-sideslip-item',
		emits: ['OptionsSideslipClick'],
		props: {
			data: {
				require: true
			},
			options: {
				type: Array,
				default: () => [{
					title: '删除',
					code: 'del',
					background: '#FF0000'
				}]
			},
		},
		computed: {
			optionWidth() {
				const width = this.options.length * 70
				return width
			}
		},
		data() {
			return {
				touchStartX: undefined,
				isTouchMove: false
			}
		},
		methods: {
			handleOptions(code) {
				this.$emit("OptionsSideslipClick", code, this.data)
			},
			touchstart(e) {
				this.touchStartX = e.changedTouches[0].clientX;
			},
			touchend(e) {
				const touchStartX = this.touchStartX
				const touchEndX = e.changedTouches[0].clientX;

				if (touchStartX - touchEndX > 80) {
					this.isTouchMove = true
				} else {
					this.isTouchMove = false
				}
			},
			resetTouch() {
				this.isTouchMove = false
			},

		}
	}
</script>

<style lang="scss" scoped>
	.container-wrapper {
		position: relative;
		box-sizing: border-box;
		transition: all 0.3s;

		.container {
			position: relative;
			width: 100%;
		}

		.options-wrapper {
			position: absolute;
			top: 0;
			right: 0;
			height: 100%;
			display: flex;
			align-items: center;
			justify-content: space-around;
			z-index: 999;
			color: white;

			.option-title {
				background-color: red;
				height: 100%;
				width: 70px;
				display: flex;
				align-items: center;
				justify-content: center;
			}
		}
	}
</style>