具有可读性的参考标志

* d3.axisTop - create a new top-oriented axis generator.
    创建一个新的上方位的轴generator
* d3.axisRight - create a new right-oriented axis generator.
    创建一个新的右方位的轴generator
* d3.axisBottom - create a new bottom-oriented axis generator.
    创建一个新的下方位的轴generator
* d3.axisLeft - create a new left-oriented axis generator.
    创建一个新的左方位的轴generator
* axis - generate an axis for the given selection.
    为给定的选择器创建一个轴
* axis.scale - set the scale.
    设置比例
* axis.ticks - customize how ticks are generated and formatted.
    定制ticks如何生成与格式化
* axis.tickArguments - customize how ticks are generated and formatted.
    定制ticks如何生成与格式化
* axis.tickValues - set the tick values explicitly.
    设置tick定义的值
* axis.tickFormat - set the tick format explicitly.
    设置tick格式化的值
* axis.tickSize - set the size of the ticks.
    设置tick的范围
* axis.tickSizeInner - set the size of inner ticks.
    设置tick的Inner范围
* axis.tickSizeOuter - set the size of outer (extent) ticks.
    设置tick的Outer范围
* axis.tickPadding - set the padding between ticks and labels.
    设置tick的Padding范围
    
具有可读性的参考标志

* d3.axisTop - create a new top-oriented axis generator.
    创建一个新的上方位的轴generator
* d3.axisRight - create a new right-oriented axis generator.
    创建一个新的右方位的轴generator
* d3.axisBottom - create a new bottom-oriented axis generator.
    创建一个新的下方位的轴generator
* d3.axisLeft - create a new left-oriented axis generator.
    创建一个新的左方位的轴generator
* axis - generate an axis for the given selection.
    为给定的选择器创建一个轴
* axis.scale - set the scale.
    设置比例
* axis.ticks - customize how ticks are generated and formatted.
    定制ticks如何生成与格式化
* axis.tickArguments - customize how ticks are generated and formatted.
    定制ticks如何生成与格式化
* axis.tickValues - set the tick values explicitly.
    设置tick定义的值
* axis.tickFormat - set the tick format explicitly.
    设置tick格式化的值
* axis.tickSize - set the size of the ticks.
    设置tick的范围
* axis.tickSizeInner - set the size of inner ticks.
    设置tick的Inner范围
* axis.tickSizeOuter - set the size of outer (extent) ticks.
    设置tick的Outer范围
* axis.tickPadding - set the padding between ticks and labels.
    设置tick的Padding范围
    

# d3-axis
轴组件呈现人类可读的标度参考标记。这减轻了数据可视化中较繁琐的任务之一。

## 安装
如果您使用NPM，`npm install d3-axis`。否则，请下载[最新版本](https://github.com/d3/d3-axis/releases/tag/v1.0.8)。您也可以直接从[d3js.org](https://d3js.org/)加载，作为独立的库或D3 4.0的一部分。（为了有效，您还需要使用d3-scale和d3-selection，但这些都是软依赖项。）支持AMD，CommonJS和vanilla环境。在vanillaJS中，一个d3全球性的出口：
```
<script src="https://d3js.org/d3-axis.v1.min.js"></script>
<script>

var axis = d3.axisLeft(scale);

</script>
```
[在浏览器中尝试d3轴。](https://npm.runkit.com/d3-axis)

# API参考
不管方向如何，坐标轴始终都在原点上。要相对于图表更改轴的位置，请在包含元素上指定一个[transform属性](http://www.w3.org/TR/SVG/coords.html#TransformAttribute)。例如：
```
d3.select("body").append("svg")
    .attr("width", 1440)
    .attr("height", 30)
  .append("g")
    .attr("transform", "translate(0,30)")
    .call(axis);
```
轴创建的元素被视为其公共API的一部分。您可以应用外部样式表或修改生成的轴元素来[自定义轴外观](https://bl.ocks.org/mbostock/3371592)。

![](https://bl.ocks.org/mbostock/3371592)

一个轴由一个类“域” 的[路径元素](https://www.w3.org/TR/SVG/paths.html#PathElement)组成，它代表了标度域的范围，接着是代表每个标度刻度的类“tick” 的转换后的[g元素](https://www.w3.org/TR/SVG/struct.html#Groups)。每个刻度线都有一个绘制刻度[线](https://www.w3.org/TR/SVG/shapes.html#LineElement)的[线条元素](https://www.w3.org/TR/SVG/shapes.html#LineElement)和刻度标签的[文本元素](https://www.w3.org/TR/SVG/shapes.html#LineElement)。例如，这里是一个典型的底面轴：
```
<g fill="none" font-size="10" font-family="sans-serif" text-anchor="middle">
  <path class="domain" stroke="#000" d="M0.5,6V0.5H880.5V6"></path>
  <g class="tick" opacity="1" transform="translate(0.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">0.0</text>
  </g>
  <g class="tick" opacity="1" transform="translate(176.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">0.2</text>
  </g>
  <g class="tick" opacity="1" transform="translate(352.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">0.4</text>
  </g>
  <g class="tick" opacity="1" transform="translate(528.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">0.6</text>
  </g>
  <g class="tick" opacity="1" transform="translate(704.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">0.8</text>
  </g>
  <g class="tick" opacity="1" transform="translate(880.5,0)">
    <line stroke="#000" y2="6"></line>
    <text fill="#000" y="9" dy="0.71em">1.0</text>
  </g>
</g>
```
轴的方向是固定的; 改变方向，删除旧的轴并创建一个新的轴。

\# d3.axisTop(scale) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L159)  
为给定的[比例](https://github.com/d3/d3-scale)构造一个新的面向顶点的轴生成器，其中包含空的[tick参数](https://github.com/d3/d3-axis/blob/master/README.md#axis_ticks)，[tick大小](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickSize)为6，[padding](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickPadding)为3.在此方向上，在水平域路径上方绘制刻度线。

\# d3.axisRight(scale) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L163)  
为给定的[比例](https://github.com/d3/d3-scale)构造一个新的右向顶点的轴生成器，其中包含空的[tick参数](https://github.com/d3/d3-axis/blob/master/README.md#axis_ticks)，[tick大小](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickSize)为6，[padding](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickPadding)为3.在此方向上，在水平域路径上方绘制刻度线。

\# d3.axisBottom(scale) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L167)  
为给定的[比例](https://github.com/d3/d3-scale)构造一个新的面向底部的轴生成器，其中包含空的[tick参数](https://github.com/d3/d3-axis/blob/master/README.md#axis_ticks)，[tick大小](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickSize)为6，[padding](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickPadding)为3.在此方向上，在水平域路径上方绘制刻度线。

\# d3.axisRight(scale) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L171)  
为给定的[比例](https://github.com/d3/d3-scale)构造一个新的左向顶点的轴生成器，其中包含空的[tick参数](https://github.com/d3/d3-axis/blob/master/README.md#axis_ticks)，[tick大小](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickSize)为6，[padding](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickPadding)为3.在此方向上，在水平域路径上方绘制刻度线。

\# axis(context) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L40)  
将轴渲染到给定的上下文中，该上下文可以是SVG容器（SVG或G元素）的[选择](https://www.w3.org/TR/SVG/struct.html#Groups)，也可以是相应的[过渡](https://github.com/d3/d3-transition)。

\# axis.ticks(arguments…) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L40)  
\# axis.ticks([count[, specifier]])
\# axis.ticks([interval[, specifier]])
设置将要传递的参数，并在[渲染](https://github.com/d3/d3-axis/blob/master/README.md#_axis)轴时[scale.ticks](https://github.com/d3/d3-scale/blob/master/README.md#continuous_ticks)和[scale.tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat)，并返回轴生成器。参数的含义依赖于轴线刻度类型：最常见的是，参数是一个建议的ticks的数目（或时间间隔为时间尺度），和可选的格式指定符来定制ticks值是如何格式化的。
如果scale没有设置scale.ticks与band和point scales，这个方法将没有效果。
要明确设置刻度值，请使用[axis .tickValues](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickValues)。要明确设置刻度格式，请使用[axis .tickFormat](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickFormat)。

例如，要在线性标度上生成二十个具有SI前缀格式的刻度，如下：
```
axis.ticks(20, "s");
```
要每十五分钟产生一个时间刻度，如下：
```
axis.ticks(d3.timeMinute.every(15));
```
这个方法也是[axis .tickArguments](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickArguments)的一个简写函数。例如，这个：
```
axis.ticks(10);
```
相当于：
```
axis.tickArguments([10]);
```

\# axis.tickArguments([arguments]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L128)  
设置将要传递的参数，并在[渲染](https://github.com/d3/d3-axis/blob/master/README.md#_axis)轴时[scale.ticks](https://github.com/d3/d3-scale/blob/master/README.md#continuous_ticks)和[scale.tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat)，并返回轴生成器。参数的含义依赖于轴线刻度类型：最常见的是，参数是一个建议的ticks的数目（或时间间隔为时间尺度），和可选的格式指定符来定制ticks值是如何格式化的。
如果scale没有设置scale.ticks与band和point scales，这个方法将没有效果。
要明确设置刻度值，请使用[axis .tickValues](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickValues)。要明确设置刻度格式，请使用[axis .tickFormat](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickFormat)。
如果参数没有指定，返回当前ticks参数，其缺省为空数组。
例如，要在线性标度上生成二十个具有SI前缀格式的刻度，如下：
```
axis.ticks(20, "s");
```
要每十五分钟产生一个时间刻度，如下：
```
axis.ticks(d3.timeMinute.every(15));
```
另请参阅[axis .ticks](https://github.com/d3/d3-axis/blob/master/README.md#axis_ticks)。

\# axis.tickValues([values]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L132)  
如果指定了values数组，则指定的值将用于ticks，而不是使用scale的自动tick生成器。如果值为空，则清除任何先前设置的显式刻度值，然后返回到刻度的刻度生成器。如果未指定值，则返回当前的刻度值，默认值为null。例如，要以特定值生成ticks：
```
var xAxis = d3.axisBottom(x)
    .tickValues([1, 2, 3, 5, 8, 13, 21]);
```
明确的刻度值先于[axis .tickArguments](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickArguments)设置的刻度参数。但是，如果没有设置刻度格式，任何刻度参数仍然会传递给刻度的[tickFormat](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickFormat)函数。

\# axis.tickFormat([format]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L136)  
如果格式指定，设定蜱格式函数并返回轴线。如果未指定format，则返回当前格式化的函数，默认为null。空格式表示应该使用比例的默认格式化程序，它是通过调用[scale .tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat)生成的。在这种情况下，通过指定的参数[axis .tickArguments](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickArguments)同样传递到scale的[tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat)。
请参阅[d3格式](https://github.com/d3/d3-format)和[d3时间格式](https://github.com/d3/d3-time-format)以获取帮助创建格式化程序的信息。例如，要使用逗号分组来显示数千个整数：
```
axis.tickFormat(d3.format(",.0f"));
```
更常见的是，格式说明符被传递给axis.ticks：
```
axis.ticks(10, ",f");
```
这具有基于tick间隔自动设置格式精度的优点。

\# axis.tickSize([size]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L140)  
如果指定了大小，则将内部和外部刻度尺寸设置为指定的值并返回轴。如果未指定大小，则返回当前的内部刻度大小，默认值为6。

\# axis.tickSizeInner([size]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L144)  
如果指定了大小，则将内部刻度大小设置为指定的值并返回轴。如果未指定大小，则返回当前的内部刻度大小，默认值为6.内部刻度大小控制刻度线的长度，与轴的原始位置偏移。

\# axis.tickSizeOuter([size]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L148)  
如果指定了大小，则将外部刻度大小设置为指定的值并返回坐标轴。如果未指定大小，则返回当前的外部刻度大小，默认值为6.外部刻度大小控制域路径的平方结束长度，偏离轴的原始位置。因此，“outer ticks”实际上不是ticks，而是部分路径，它们的位置由相关尺度的域范围决定。因此，外部ticks可能与第一个或最后一个内部ticks重叠。外部刻度大小为0时会抑制域路径的方形末端，而不会产生直线。

\# axis.tickSizeOuter([size]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L152)  
如果填充被指定，设定填充到以像素为单位指定的值，并返回轴线。如果没有指定填充，则返回默认为3个像素的当前填充。



