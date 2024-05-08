# lidy-sideslip 侧滑操作

lidy-sideslip 可侧拉的列表组件,多端兼容。

## 安装方式

本组件符合[easycom](https://uniapp.dcloud.io/collocation/pages?id=easycom)规范，`HBuilderX 2.5.5`起，只需将本组件导入项目，在页面`template`中即可直接使用，无需在页面中`import`和注册`components`。

## 基本用法
- vue结构

```vue
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
```
- JavaScript结构


```js
export default {
    data() {
        return {
            list: ['第一条数据','第二条数据','第三条数据','第四条数据','第五条数据','第六条数据'],
            options: [
                {title: '关注',code: 'follow',background: '#FBC21C'},
                {title: '删除',code: 'del',background: '#FF0000'}
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
```
- css结构

```css
.card {
    height: 45px;
    display: flex;
    align-items: center;
    padding-left: 12px;
}
```

## API

### lidy-sideslip-item Props

|       属性名       |  类型  |       默认值       |                  说明                   |
| :----------------: | :----: | :----------------: | :-------------------------------------: |
|        data        | Object |   必填，无默认值   |              每条列表数据               |
|      options       | Array  | 默认为单个删除按钮 | 操作列配置,为多个对象数组,对象属性如下: |
|   options.title    | String |   必填，无默认值   |              右侧按钮标题               |
|    options.code    | String |   必填，无默认值   |            右侧按钮唯一编码             |
| options.background | String |   必填，无默认值   |            右侧按钮背景颜色             |

### ListItem Events

|       事件名称       |       说明       |                返回参数                |
| :------------------: | :--------------: | :------------------------------------: |
| OptionsSideslipClick | 右侧按钮点击事件 | e=>{code:按钮唯一编码,data:当前行数据} |

完整演示代码下载: 
