# wx-charts
微信小程序图表工具，charts for WeChat small app

基于canvas绘制，体积小巧

**支持图表类型**
- 饼图 `pie`
- 线图 `line`
- 柱状图 `column`
- 区域图 `area`

**高清显示**

设置canvas的尺寸为2倍大小，然后缩小到50%，建议都进行这样的设置，图表本身绘制时是按照高清显示配置的，不然整体效果会偏大

```css
.canvas {
    width: 200%;
    height: 600px;
    transform: scale(0.5)
}
```

代码分析 [Here](https://segmentfault.com/a/1190000007649376)

# 参数说明
`opts` Object

`opts.canvasId` String **required** 微信小程序canvas-id

`opts.width` Number **required** canvas宽度，单位为px

`opts.height` Number **required** canvas高度，单位为px

`opts.type` String **required** 图表类型，可选值为`pie`, `line`, `column`, `area`

`opts.categories` Array **required** *(饼图不需要)* 数据类别分类

`opts.yAxisFormat` Function Y轴显示自定义格式内容

`opts.dataLabel` Boolean default `true` 是否在图表中显示数据内容值

`opts.series` Array **required** 数据列表

**数据列表每项结构定义**

`dataItem` Object

`dataItem.data` Array **required** *(饼图为Number)* 数据

`dataItem.color` String 例如`#7cb5ec` 不传入则使用系统默认配色方案

`dataItem.name` String 数据名称

`dateItem.format` Function 自定义显示数据内容

# Example

### pie chart

```javascript
var Charts = require('charts.js');
new Charts({
    canvasId: 'pieCanvas',
    type: 'pie',
    series: [{
        name: '成交量1',
        data: 15,
    }, {
        name: '成交量2',
        data: 35,
    }, {
        name: '成交量3',
        data: 78,
    }, {
        name: '成交量4',
        data: 63,
    }],
    width: 640,
    height: 400,
    dataLabel: false
});
```
![pieChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/pie.png)

### line chart

```javascript
new Charts({
    canvasId: 'lineCanvas',
    type: 'line',
    categories: ['2016-08', '2016-09', '2016-10', '2016-11', '2016-12', '2017'],
    series: [{
        name: '成交量1',
        data: [15, 20, 45, 37, 4, 80],
        format: function (val) {
            return val.toFixed(2) + '万';
        }
    }, {
        name: '成交量2',
        data: [70, 40, 65, 100, 34, 18],
        format: function (val) {
            return val.toFixed(2) + '万';
        }
    }],
    yAxisFormat: function (val) {
        return val + '万';
    },
    width: 640,
    height: 400
});
```

![lineChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/line.png)

### columnChart

```javascript
new Charts({
    canvasId: 'columnCanvas',
    type: 'column',
    categories: ['2016-08', '2016-09', '2016-10', '2016-11', '2016-12', '2017'],
    series: [{
        name: '成交量1',
        data: [15, 20, 45, 37, 4, 80]
    }, {
        name: '成交量2',
        data: [70, 40, 65, 100, 34, 18]
    }, {
        name: '成交量3',
        data: [70, 40, 65, 100, 34, 18]
    }, {
        name: '成交量4',
        data: [70, 40, 65, 100, 34, 18]
    }],
    yAxisFormat: function (val) {
        return val + '万';
    },
    width: 640,
    height: 400,
    dataLabel: false
});
```

![columnChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/column.png)

### areaChart

```javascript
new Charts({
    canvasId: 'areaCanvas',
    type: 'area',
    categories: ['2016-08', '2016-09', '2016-10', '2016-11', '2016-12', '2017'],
    series: [{
        name: '成交量1',
        data: [70, 40, 65, 100, 34, 18],
        format: function (val) {
            return val.toFixed(2) + '万';
        }
    }, {
        name: '成交量2',
        data: [15, 20, 45, 37, 4, 80],
        format: function (val) {
            return val.toFixed(2) + '万';
        }
    }],
    yAxisFormat: function (val) {
        return val + '万';
    },
    width: 640,
    height: 400
});
```

![areaChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/area.png)

# TodoList

- [x] add legend
- [ ] add animation
