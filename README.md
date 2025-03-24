## 项目描述

大屏可视化 Vue3+vite版本，
公司有大屏可视化的产品需求，故网上找了资源并在原有的基础上进行二次开发，主要内容调整还得是后端前端基本就是拿数据然后过滤处理后加入到chart
另外还搞了个二次开发的低代码平台可视化项目，但先这样了，因为是公司自研项目，所以不方便把太多项目内容放进来，目前只展示前端部分。

#### 部分介绍

- 项目需要全屏展示（按 F11），有可自适应按钮切换操作。

- 项目部分区域使用了全局注册方式，增加了打包体积，在实际运用中请使用 **按需引入**。

- 项目环境：Vite + Vue3,Echarts,Npm,Node,axios,mock。

- 在项目public目录下存放地图数据合集，根据地市编存放。

- 本机项目 node -v 19.9.0

### 采用自适应组件方式，

###  滚动设置，自适应设置 

项目中可以进行滚动配置，内容是否滚动

点击右上角设置按钮


##  2、主要文件介绍

| 文件              | 作用/功能                                                    |
| ----------------- | ------------------------------------------------------------ |
| main.js           | 主目录文件，引入 Echart/DataV 等文件                         |
| utils             | 工具函数与 mixins 函数等                                     |
| views/ home.vue   | 项目主结构                                                   |
| views/其余文件    | 界面各个区域组件（按照位置来命名）                           |
| assets            | 静态资源目录，放置 logo 与背景图片                           |
| assets / css/     | 通用 CSS 文件，全局项目快捷样式调节                          |
| components/echart | 所有 echart 图表（按照位置来命名）                           |
| common/...        | 全局封装的 ECharts 和 flexible 插件代码（适配屏幕尺寸，可定制化修改） |
| api/api.js        | 接口封装文件                                                 |
| mock              | 模拟数据接口地址                                             |

###  

## 使用介绍

### 安装

```npm
npm install   
```
### 启动

```npm
npm run dev
```

### 打包编译

```npm
npm run build
```

### 取消mock模拟数据

```javascript
// src\main.ts文件
把下面两行代码注释掉就可以了。
import { mockXHR } from "@/mock/index";
mockXHR()
```

## 

## 公用组件

封装了除面条外个别用到的组件

### 自适应缩放组件

#### 注意

采用Scale方式，会自动给组件父元素添加overflow:hidden 

#### 使用

```vue
<template>
  <scale-screen width="1920" height="1080">
    <div>
   			content
    </div>
  </scale-screen>
</template>

<script>
import ScaleScreen from 'scale-screen'

export default {
  name:'Demo',
  components:{
    VScaleScreen
  }
}
</script>
```

#### API

| 属性         | 说明                                                         | 类型                             | 默认值 |
| ------------ | ------------------------------------------------------------ | -------------------------------- | ------ |
| selfAdaption | 是否进行自适应                                               | Boolean                          | true   |
| width        | 大屏宽度                                                     | `Number` or `String`             | 1920   |
| height       | 大屏高度                                                     | `Number` or `String`             | 1080   |
| autoScale    | 自适应配置，配置为boolean类型时，为启动或者关闭自适应，配置为对象时，若x为true，x轴产生边距，y为true时，y轴产生边距，启用fullScreen时此配置失效 | Boolean or {x:boolean,y:boolean} | true   |
| delay        | 窗口变化防抖延迟时间                                         | Number                           | 500    |
| fullScreen   | 全屏自适应，启用此配置项时会存在拉伸效果，同时autoScale失效，非必要情况下不建议开启 | Boolean                          | false  |
| boxStyle     | 修改容器样式，如居中展示时侧边背景色，符合Vue双向绑定style标准格式 | Object                           | null   |
| wrapperStyle | 修改自适应区域样式，符合Vue双向绑定style标准格式             | Object                           | null   |


###  外边框

因为我的项目外边框几乎一样，还有title,所以封装了此组件。

根据自己需求更改，更换外边框（src\components\item-wrap\item-wrap.vue）下更换。

```vue
<ItemWrap
    title="my title"
    >
       <div>who?</div>
</ItemWrap>
```

| 参数  | 描述 | 默认值 |  类型  | 可选值 |
| :---: | :--: | :----: | :----: | :----: |
| title | 标头 |   -    | string |   -    |

### CountUp 数字滚动

以下属性同 coutup.js 配置项（same as countup.js properties）

#### Props

| Name     | Type             | Default | Description                                                  |
| -------- | ---------------- | ------- | ------------------------------------------------------------ |
| endVal   | Number \| String | -       | 结束值                                                       |
| startVal | Number \| String | 0       | 起始值                                                       |
| duration | Number           | 2.5     | 动画时长，单位：秒                                           |
| options  | Object           | -       | [countUp.js](https://github.com/inorganik/countUp.js) options 配置项 |

以下为组件特有属性（extension properties）

| Name     | Type              | Default | Description                   |
| -------- | ----------------- | ------- | ----------------------------- |
| autoplay | Boolean           | true    | 是否自动计数                  |
| loop     | Boolean \| Number | false   | 循环次数，有限次数 / 无限循环 |
| delay    | Number            | 0       | loop 循环的间隔时间，单位：秒 |

#### 插槽（slots）

| Name   | Description |
| ------ | ----------- |
| prefix | 前缀        |
| suffix | 后缀        |

#### 事件（Events）

| Name      | Description                | return       |
| --------- | -------------------------- | ------------ |
| @init     | CountUp 实例初始化完成触发 | CountUp 实例 |
| @finished | 计数结束时触发             | -            |

#### countup.js 配置项说明
```ts
interface CountUpOptions {
  startVal?: number // number to start at (0) 开始数值，默认 0
  decimalPlaces?: number // number of decimal places (0) 小数点 位数
  duration?: number // animation duration in seconds (2) 动画时长
  useGrouping?: boolean // example: 1,000 vs 1000 (true) 是否使用千分位
  useEasing?: boolean // ease animation (true) 是否开启动画过渡，默认动画函数为easeOutExpo 
  smartEasingThreshold?: number // smooth easing for large numbers above this if useEasing (999)
  smartEasingAmount?: number // amount to be eased for numbers above threshold (333)
  separator?: string // grouping separator (',') 千分位分隔符
  decimal?: string // decimal ('.') 小数点分隔符
  // easingFn: easing function for animation (easeOutExpo) 动画函数
  easingFn?: (t: number, b: number, c: number, d: number) => number
  formattingFn?: (n: number) => string // this function formats result 格式化结果
  prefix?: string // text prepended to result 数值前缀
  suffix?: string // text appended to result 数值后缀
  numerals?: string[] // numeral glyph substitution 数字符号替换 0 - 9，例如替换为 [a,b,c,d,e,f,g,h,i,j]
  enableScrollSpy?: boolean // start animation when target is in view 在可视范围内才开始动画
  scrollSpyDelay?: number // delay (ms) after target comes into view  目标进入可视范围内后的延迟时间(毫秒)
}
```

###  胶囊柱图

#### Props

|  属性  |   说明   |      类型       |          可选值           | 默认值  |
| :----: | :------: | :-------------: | :-----------------------: | :-----: |
|  data  |  柱数据  | `Array<Object>` |   [data属性](#data属性)   |  `[]`   |
| config | 基础配置 |     Object      | [config属性](#config属性) | `false` |

#### config属性

|   属性    |   说明   |      类型       | 可选值 | 默认值  |
| :-------: | :------: | :-------------: | :----: | :-----: |
|   unit    |   单位   |    `String`     |  ---   |  `''`   |
|  colors   |  环颜色  | `Array<String>` |  [1]   |   [2]   |
| showValue | 显示数值 |    `Boolean`    |  ---   | `false` |

#### 注释config注释

[1] 颜色支持`hex|rgb|rgba|颜色关键字`等四种类型。

[2] 默认配色为`['#37a2da', '#32c5e9', '#67e0e3', '#9fe6b8', '#ffdb5c', '#ff9f7f', '#fb7293']`。

#### data属性

| 属性  |   说明   |   类型   | 可选值 | 默认值 |
| :---: | :------: | :------: | :----: | :----: |
| name  |  柱名称  | `String` |  ---   |  ---   |
| value | 柱对应值 | `Number` |  ---   |  ---   |

## 中间地图

### 南海显隐控制

 根据需求来，**修改此值请刷新页面**

```indexs/center-map.vue``` 文件中```isSouthChinaSea```变量 默认不显示南海(false),为```true```的时候显示南海

```
isSouthChinaSea:false,//默认不显示南海，改为true可显示南海
```

## end
Thanks for the open source
