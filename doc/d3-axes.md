[文档源链接](https://github.com/d3/d3/blob/master/API.md#axes-d3-axis)

# d3-axis
The axis component renders human-readable reference marks for [scales](https://github.com/d3/d3-scale). This alleviates one of the more tedious tasks in visualizing data.

轴组件为[比例](https://github.com/d3/d3-scale)渲染可读的参考标记。这减轻了数据可视化中较为繁琐的任务之一。

## Installing
If you use NPM, `npm install d3-polygon`. Otherwise, download the [latest release](https://github.com/d3/d3-polygon/releases/latest). You can also load directly from [d3js.org](https://d3js.org), either as a [standalone library](https://d3js.org/d3-polygon.v1.min.js) or as part of [D3 4.0](https://github.com/d3/d3). AMD, CommonJS, and vanilla environments are supported. In vanilla, a `d3` global is exported:

```
<script src="https://d3js.org/d3-axis.v1.min.js"></script>
<script>

var axis = d3.axisLeft(scale);

</script>
```
[Try d3-axis in your browser.](https://npm.runkit.com/d3-axis)

# API Reference
Regardless of orientation, axes are always rendered at the origin. To change the position of the axis with respect to the chart, specify a [transform attribute](http://www.w3.org/TR/SVG/coords.html#TransformAttribute) on the containing element. For example:

不管方向如何，坐标轴的起点是在原点上。要相对于图表更改轴的位置，请在包含元素上指定一个[transform属性](http://www.w3.org/TR/SVG/coords.html#TransformAttribute)。例如：
```
d3.select("body").append("svg")
    .attr("width", 1440)
    .attr("height", 30)
  .append("g")
    .attr("transform", "translate(0,30)")
    .call(axis);
```
The elements created by the axis are considered part of its public API. You can apply external stylesheets or modify the generated axis elements to [customize the axis appearance](https://bl.ocks.org/mbostock/3371592).

创建坐标轴元素是公共API的一部分。您可以应用外部样式表或修改生成的轴元素来[自定义轴外观](https://bl.ocks.org/mbostock/3371592)。

<img alt="Custom Axis" src="https://raw.githubusercontent.com/d3/d3-axis/master/img/custom.png" width="420" height="219" style="max-width:100%;">

An axis consists of a path element of class “domain” representing the extent of the scale’s domain, followed by transformed g elements of class “tick” representing each of the scale’s ticks. Each tick has a line element to draw the tick line, and a text element for the tick label. For example, here is a typical bottom-oriented axis:

一个轴由一class为“domain” 的[path](https://www.w3.org/TR/SVG/paths.html#PathElement)组成，它代表了标度域的范围，接着是代表每个标度刻度的类“tick” 的转换后的[g element](https://www.w3.org/TR/SVG/struct.html#Groups)。每个刻度线都有一个绘制刻度[line](https://www.w3.org/TR/SVG/shapes.html#LineElement)的[line element](https://www.w3.org/TR/SVG/shapes.html#LineElement)和刻度标签的[text element](https://www.w3.org/TR/SVG/shapes.html#LineElement)。例如，这里是一个典型的底面轴：
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
The orientation of an axis is fixed; to change the orientation, remove the old axis and create a new axis.

轴的方向是固定的; 如需改变方向，可以删除旧的轴并创建一个新的轴。

<a name="user-content-axis_axisTop" href="#axis_axisTop">#</a> d3.axisTop(scale) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L159)  
Constructs a new top-oriented axis generator for the given scale, with empty tick arguments, a tick size of 6 and padding of 3. In this orientation, ticks are drawn above the horizontal domain path.  

为给定的[scale](https://github.com/d3/d3-scale)构造一个新的面向顶部的轴生成器，其中包含空的 tick arguments](https://github.com/d3/d3-axis/blob/master/README.md#axis_ticks)，[tick size](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickSize)为6，[padding](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickPadding)为3.在此方向上，在水平域路径上方绘制刻度线。
  
<a name="user-content-axis_axisRight" href="#axis_axisRight">#</a> d3.axisRight(scale) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L163)  
Constructs a new right-oriented axis generator for the given scale, with empty tick arguments, a tick size of 6 and padding of 3. In this orientation, ticks are drawn to the right of the vertical domain path.

为给定的[scale](https://github.com/d3/d3-scale)构造一个新的右向顶点的轴生成器，其中包含空的[tick arguments](https://github.com/d3/d3-axis/blob/master/README.md#axis_ticks)，[tick size](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickSize)为6，[padding](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickPadding)为3.在此方向上，在水平域路径上方绘制刻度线。

<a name="user-content-axis_axisBottom" href="#axis_axisBottom">#</a> d3.axisBottom(scale) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L167)  
Constructs a new bottom-oriented axis generator for the given scale, with empty tick arguments, a tick size of 6 and padding of 3. In this orientation, ticks are drawn below the horizontal domain path.

为给定的[scale](https://github.com/d3/d3-scale)构造一个新的面向底部的轴生成器，其中包含空的[tick arguments](https://github.com/d3/d3-axis/blob/master/README.md#axis_ticks)，[tick size](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickSize)为6，[padding](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickPadding)为3.在此方向上，在水平域路径上方绘制刻度线。

<a name="user-content-axis_axisRight" href="#axis_axisRight">#</a> d3.axisRight(scale) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L171)  
Constructs a new left-oriented axis generator for the given scale, with empty tick arguments, a tick size of 6 and padding of 3. In this orientation, ticks are drawn to the left of the vertical domain path.

为给定的[scale](https://github.com/d3/d3-scale)构造一个新的左向顶点的轴生成器，其中包含空的[tick arguments](https://github.com/d3/d3-axis/blob/master/README.md#axis_ticks)，[tick size](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickSize)为6，[padding](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickPadding)为3.在此方向上，在水平域路径上方绘制刻度线。

<a name="user-content-axis_context" href="#axis_context">#</a> axis(context) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L40)  
Render the axis to the given context, which may be either a selection of SVG containers (either SVG or G elements) or a corresponding transition.

将轴渲染到给定的上下文中，该上下文可以是SVG容器（SVG或G元素）的[选择](https://www.w3.org/TR/SVG/struct.html#Groups)，也可以是相应的[过渡](https://github.com/d3/d3-transition)。

<a name="user-content-axis_scale" href="#axis_scale">#</a> scale(context) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L120)  
If scale is specified, sets the scale and returns the axis. If scale is not specified, returns the current scale.

如果[scale](https://www.w3.org/TR/SVG/struct.html#Groups)存在，设置scale并返回axis。如果scale不存在，则返回当前scale。
将轴渲染到给定的上下文中，该上下文可以是SVG容器（SVG或G元素）的，也可以是相应的[过渡](https://github.com/d3/d3-transition)。



<a href="#axis_ticks">#</a> axis.ticks(arguments…) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L40)  
<a href="#axis_ticks">#</a> axis.ticks([count[, specifier]])
<a href="#axis_ticks">#</a> axis.ticks([interval[, specifier]])

Sets the arguments that will be passed to scale.ticks and scale.tickFormat when the axis is rendered, and returns the axis generator. The meaning of the arguments depends on the axis’ scale type: most commonly, the arguments are a suggested count for the number of ticks (or a time interval for time scales), and an optional format specifier to customize how the tick values are formatted.

This method has no effect if the scale does not implement scale.ticks, as with band and point scales. To set the tick values explicitly, use axis.tickValues. To set the tick format explicitly, use axis.tickFormat.

设置将要传递的参数，并在[rendered](https://github.com/d3/d3-axis/blob/master/README.md#_axis)轴时[scale.ticks](https://github.com/d3/d3-scale/blob/master/README.md#continuous_ticks)和[scale.tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat)，并返回轴生成器。参数的含义依赖于轴线刻度类型：最常见的是，参数是一个建议的ticks的数目（或时间间隔为时间尺度），和可选的格式指定符来定制ticks值是如何格式化的。
如果scale没有设置scale.ticks与band和point scales，这个方法将不会生效。
要设置刻度值，请使用[axis .tickValues](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickValues)。要设置刻度格式，请使用[axis .tickFormat](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickFormat)。

For example, to generate twenty ticks with SI-prefix formatting on a linear scale, say:

例如，要在线性标度上生成二十个具有SI前缀格式的刻度，如下：
```
axis.ticks(20, "s");
```

To generate ticks every fifteen minutes with a time scale, say:

要每十五分钟产生一个时间刻度，如下：
```
axis.ticks(d3.timeMinute.every(15));
```

This method is also a convenience function for axis.tickArguments. For example, this:

这个方法也是[axis .tickArguments](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickArguments)的一个简写函数。例如，这个：
```
axis.ticks(10);
```

Is equivalent to:

相当于：
```
axis.tickArguments([10]);
```

<a name="user-content-axis_tickArguments" href="#axis_tickArguments">#</a> axis.tickArguments([arguments]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L128)  

If arguments is specified, sets the arguments that will be passed to scale.ticks and [scale.tickFormat](https://github.com/d3/d3-axis/blob/master/README.md#_axis) when the axis is [rendered](https://github.com/d3/d3-scale/blob/master/README.md#continuous_ticks)和[scale.tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat), and returns the axis generator. The meaning of the arguments depends on the [axis’ scale] type: most commonly, the arguments are a suggested count for the number of ticks (or a [time interval](https://github.com/d3/d3-time) for time scales), and an optional format [specifier](https://github.com/d3/d3-format) to customize how the tick values are formatted.

If arguments is specified, this method has no effect if the scale does not implement scale.ticks, as with band and point scales. To set the tick values explicitly, use axis.tickValues. To set the tick format explicitly, use axis.tickFormat.

If arguments is not specified, returns the current tick arguments, which defaults to the empty array.

如果参数已设置，并在[render](https://github.com/d3/d3-axis/blob/master/README.md#_axis)轴时[scale.ticks](https://github.com/d3/d3-scale/blob/master/README.md#continuous_ticks)和[scale.tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat)，并返回轴生成器。参数的含义依赖于轴线刻度类型：最常见的是，参数是一个建议的ticks的数目（或[时间间隔](https://github.com/d3/d3-time)为时间尺度），和可选的格式[指定符]((https://github.com/d3/d3-format))来定制ticks值是如何格式化的。

如果参数是缺省的，scale.ticks与band和point scales，这个方法将不会生效。
要明确设置刻度值，请使用[axis .tickValues](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickValues)。要明确设置刻度格式，请使用[axis .tickFormat](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickFormat)。
如果参数是缺省的，返回当前ticks参数，其缺省为空数组。

For example, to generate twenty ticks with SI-prefix formatting on a linear scale, say:

例如，要在线性标度上生成二十个具有SI前缀格式的刻度，如下：
```
axis.ticks(20, "s");
```

To generate ticks every fifteen minutes with a time scale, say:

要每十五分钟产生一个时间刻度，如下：
```
axis.ticks(d3.timeMinute.every(15));
```

See also [axis.ticks](https://github.com/d3/d3-axis/blob/master/README.md#axis_ticks).

另请参阅[axis .ticks](https://github.com/d3/d3-axis/blob/master/README.md#axis_ticks)。

<a name="user-content-axis_tickValues" href="#axis_tickValues">#</a> axis.tickValues([values]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L132)  

If a values array is specified, the specified values are used for ticks rather than using the scale’s automatic tick generator. If values is null, clears any previously-set explicit tick values and reverts back to the scale’s tick generator. If values is not specified, returns the current tick values, which defaults to null. For example, to generate ticks at specific values:

如果指定了values数组，则指定的值将用于ticks，而不是使用scale的自动tick生成器。如果值为空，则清除任何先前设置的显式刻度值，然后返回到刻度的刻度生成器。如果未指定值，则返回当前的刻度值，默认值为null。例如，要以特定值生成ticks：
```
var xAxis = d3.axisBottom(x)
    .tickValues([1, 2, 3, 5, 8, 13, 21]);
```
The explicit tick values take precedent over the tick arguments set by axis.tickArguments. However, any tick arguments will still be passed to the scale’s tickFormat function if a tick format is not also set.

明确的刻度值先于[axis .tickArguments](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickArguments)设置的刻度参数。但是，如果没有设置刻度格式，任何刻度参数仍然会传递给刻度的[tickFormat](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickFormat)函数。

<a name="user-content-axis_tickFormat" href="#axis_tickFormat">#</a> axis.tickFormat([format]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L136)  

If format is specified, sets the tick format function and returns the axis. If format is not specified, returns the current format function, which defaults to null. A null format indicates that the scale’s default formatter should be used, which is generated by calling scale.tickFormat. In this case, the arguments specified by axis.tickArguments are likewise passed to scale.tickFormat.

See d3-format and d3-time-format for help creating formatters. For example, to display integers with comma-grouping for thousands:

如果格式指定，设定tick格式函数并返回轴线。如果未指定format，则返回当前格式化的函数，默认为null。空格式表示应该使用比例的默认格式化程序，它是通过调用[scale .tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat)生成的。在这种情况下，通过指定的参数[axis .tickArguments](https://github.com/d3/d3-axis/blob/master/README.md#axis_tickArguments)同样传递到scale的[tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#continuous_tickFormat)。
请参阅[d3格式](https://github.com/d3/d3-format)和[d3时间格式](https://github.com/d3/d3-time-format)以获取帮助创建格式化程序的信息。例如，要使用逗号分组来显示数千个整数：
```
axis.tickFormat(d3.format(",.0f"));
```
更常见的是，格式说明符被传递给axis.ticks：
```
axis.ticks(10, ",f");
```
这具有基于tick间隔自动设置格式精度的优点。

<a name="user-content-axis_tickSize" href="#axis_tickSize">#</a> axis.tickSize([size]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L140)  

If size is specified, sets the [inner](https://github.com/d3/d3-axis#axis_tickSizeInner) and [outer](https://github.com/d3/d3-axis#axis_tickSizeOuter) tick size to the specified value and returns the axis. If size is not specified, returns the current inner tick size, which defaults to 6.

如果指定了大小，则将内部和外部刻度尺寸设置为指定的值并返回轴。如果未指定大小，则返回当前的内部刻度大小，默认值为6。

<a name="user-content-axis_tickSizeInner" href="#axis_tickSizeInner">#</a> axis.tickSizeInner([size]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L144)  

If size is specified, sets the [inner tick size to the specified value and returns the axis. If size is not specified, returns the current inner tick size, which defaults to 6. The inner tick size controls the length of the tick lines, offset from the native position of the axis.

如果size已设置，则将内部刻度大小设置为指定的值并返回轴。如果未指定大小，则返回当前的内部刻度大小，默认值为6.内部刻度大小控制刻度线的长度，与轴的原始位置偏移。

<a name="user-content-axis_tickSizeOuter" href="#axis_tickSizeOuter">#</a> axis.tickSizeOuter([size]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L148)  

If size is specified, sets the outer tick size to the specified value and returns the axis. If size is not specified, returns the current outer tick size, which defaults to 6. The outer tick size controls the length of the square ends of the domain path, offset from the native position of the axis. Thus, the “outer ticks” are not actually ticks but part of the domain path, and their position is determined by the associated scale’s domain extent. Thus, outer ticks may overlap with the first or last inner tick. An outer tick size of 0 suppresses the square ends of the domain path, instead producing a straight line.

如果size已设置，则将外部刻度大小设置为指定的值并返回坐标轴。如果size缺省，则返回当前的外部刻度大小，默认值为6.外部刻度大小控制域路径的平方结束长度，偏离原始轴的位置。因此，“outer ticks”实际上不是ticks，而是部分路径，它们的位置由相关尺度的域范围决定。因此，外部ticks可能与第一个或最后一个内部ticks重叠。外部刻度大小为0时会抑制域路径的方形末端，而不会产生直线。

<a name="user-content-axis_tickPadding" href="#axis_tickPadding">#</a> axis.tickPadding([size]) [<>](https://github.com/d3/d3-axis/blob/master/src/axis.js#L152)  

If padding is specified, sets the padding to the specified value in pixels and returns the axis. If padding is not specified, returns the current padding which defaults to 3 pixels.

如果padding已设置，设定padding到以指定值的像素为参数，并返回轴。如果padding缺省，则返回默认的3像素。



