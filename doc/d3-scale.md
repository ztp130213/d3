# d3-scale

Scales are a convenient abstraction for a fundamental task in visualization: mapping a dimension of abstract data to a visual representation. Although most often used for position-encoding quantitative data, such as mapping a measurement in meters to a position in pixels for dots in a scatterplot, scales can represent virtually any visual encoding, such as diverging colors, stroke widths, or symbol size. Scales can also be used with virtually any type of data, such as named categorical data or discrete data that requires sensible breaks.

缩放对于可视化中的基本任务来说是一个方便的抽象：将抽象数据的维映射到可视化展示。虽然大多数情况下用于定位编码定量数据，例如将测量值以米为单位映射为散点图中点的像素位置，但缩放可以表示几乎任何视觉编码，例如发散颜色，线性宽度或符号大小。比例还可以用于几乎任何类型的数据，例如命名的分类数据或需要合理中断的离散数据

For [continuous](#continuous-scales) quantitative data, you typically want a [linear scale](#linear-scales). (For time series data, a [time scale](#time-scales).) If the distribution calls for it, consider transforming data using a [power](#power-scales) or [log](#log-scales) scale. A [quantize scale](#quantize-scales) may aid differentiation by rounding continuous data to a fixed set of discrete values; similarly, a [quantile scale](#quantile-scales) computes quantiles from a sample population, and a [threshold scale](#threshold-scales) allows you to specify arbitrary breaks in continuous data.

对于连续的定量数据，您通常需要线性刻度。（对于时间序列数据，是时间尺度。）如果分布需要它，请考虑使用功率或对数刻度转换数据。量化尺度可通过连续的数据舍入到一个固定的一组离散值的辅助分化; 类似地，分位数计算来自样本总体的分位数，并且阈值规模允许您在连续数据中指定任意中断。

For discrete ordinal (ordered) or categorical (unordered) data, an [ordinal scale](#ordinal-scales) specifies an explicit mapping from a set of data values to a corresponding set of visual attributes (such as colors). The related [band](#band-scales) and [point](#point-scales) scales are useful for position-encoding ordinal data, such as bars in a bar chart or dots in an categorical scatterplot.

对于离散序数（有序）或分类（无序）数据，序数标度指定从一组数据值到相应的一组可视属性（如颜色）的显式映射。相关的波段和点标度对位置编码序数据有用，例如条形图中的条形或分类散点图中的点。

This repository does not provide color schemes; see [d3-scale-chromatic](https://github.com/d3/d3-scale-chromatic) for color schemes designed to work with d3-scale.

该存储库不提供配色方案; 请参阅d3-scale-chromatic设计用于使用d3-scale的配色方案。

Scales have no intrinsic visual representation. However, most scales can [generate](#continuous_ticks) and [format](#continuous_tickFormat) ticks for reference marks to aid in the construction of axes.

尺度没有内在的视觉表现。但是，大多数比例尺可以生成参考标记的刻度并对其进行格式化，以帮助构建坐标轴。

For a longer introduction, see these recommended tutorials:

有关更长的介绍，请参阅以下推荐的教程：

* [Introducing d3-scale](https://medium.com/@mbostock/introducing-d3-scale-61980c51545f) by Mike Bostock

* [Chapter 7. Scales](http://chimera.labs.oreilly.com/books/1230000000345/ch07.html) of *Interactive Data Visualization for the Web* by Scott Murray

* [d3: scales, and color.](http://www.jeromecukier.net/blog/2011/08/11/d3-scales-and-color/) by Jérôme Cukier

## Installing

If you use NPM, `npm install d3-scale`. Otherwise, download the [latest release](https://github.com/d3/d3-scale/releases/latest). You can also load directly from [d3js.org](https://d3js.org), either as a [standalone library](https://d3js.org/d3-scale.v2.min.js) or as part of [D3](https://github.com/d3/d3). AMD, CommonJS, and vanilla environments are supported. In vanilla, a `d3` global is exported:

```html
<script src="https://d3js.org/d3-array.v1.min.js"></script>
<script src="https://d3js.org/d3-collection.v1.min.js"></script>
<script src="https://d3js.org/d3-color.v1.min.js"></script>
<script src="https://d3js.org/d3-format.v1.min.js"></script>
<script src="https://d3js.org/d3-interpolate.v1.min.js"></script>
<script src="https://d3js.org/d3-time.v1.min.js"></script>
<script src="https://d3js.org/d3-time-format.v2.min.js"></script>
<script src="https://d3js.org/d3-scale.v2.min.js"></script>
<script>

var x = d3.scaleLinear();

</script>
```

(You can omit d3-time and d3-time-format if you’re not using [d3.scaleTime](#scaleTime) or [d3.scaleUtc](#scaleUtc).)

## API Reference

* [Continuous](#continuous-scales) ([Linear](#linear-scales), [Power](#power-scales), [Log](#log-scales), [Identity](#identity-scales), [Time](#time-scales))
* 连续（线性，功率，日志，身份，时间）
* [Sequential](#sequential-scales)
* 顺序
* [Quantize](#quantize-scales)
* 量化
* [Quantile](#quantile-scales)
* 位数
* [Threshold](#threshold-scales)
* 阈
* [Ordinal](#ordinal-scales) ([Band](#band-scales), [Point](#point-scales))
* 序数（乐队，点）

### Continuous Scales

Continuous scales map a continuous, quantitative input [domain](#continuous_domain) to a continuous output [range](#continuous_range). If the range is also numeric, the mapping may be [inverted](#continuous_invert). A continuous scale is not constructed directly; instead, try a [linear](#linear-scales), [power](#power-scales), [log](#log-scales), [identity](#identity-scales), [time](#time-scales) or [sequential color](#sequential-scales) scale.

连续缩放将连续的定量输入域映射到连续的输出范围。如果范围也是数字，映射可能会反转。连续缩放不是直接构建的; 相反，请尝试线性，功率，日志，身份，时间或顺序色阶。

<a name="_continuous" href="#_continuous">#</a> <i>continuous</i>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/continuous.js#L69 "Source")

Given a *value* from the [domain](#continuous_domain), returns the corresponding value from the [range](#continuous_range). If the given *value* is outside the domain, and [clamping](#continuous_clamp) is not enabled, the mapping may be extrapolated such that the returned value is outside the range. For example, to apply a position encoding:

给定一个值从域，返回从相应的值范围。如果给定的值在域外，并且未启用钳位，则可以外推映射，使得返回的值超出范围。例如，要应用位置编码：

```js
var x = d3.scaleLinear()
    .domain([10, 130])
    .range([0, 960]);

x(20); // 80
x(50); // 320
```

Or to apply a color encoding:

```js
var color = d3.scaleLinear()
    .domain([10, 100])
    .range(["brown", "steelblue"]);

color(20); // "#9a3439"
color(50); // "#7b5167"
```

<a name="continuous_invert" href="#continuous_invert">#</a> <i>continuous</i>.<b>invert</b>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/continuous.js#L88 "Source")

Given a *value* from the [range](#continuous_range), returns the corresponding value from the [domain](#continuous_domain). Inversion is useful for interaction, say to determine the data value corresponding to the position of the mouse. For example, to invert a position encoding:

给定一个值从范围，返回从相应的值域。反转对交互很有用，比如确定与鼠标位置相对应的数据值。例如，要反转位置编码：
    
```js
var x = d3.scaleLinear()
    .domain([10, 130])
    .range([0, 960]);

x.invert(80); // 20
x.invert(320); // 50
```

If the given *value* is outside the range, and [clamping](#continuous_clamp) is not enabled, the mapping may be extrapolated such that the returned value is outside the domain. This method is only supported if the range is numeric. If the range is not numeric, returns NaN.

如果给定值超出范围，并且钳位未启用，则可以外推映射，使得返回的值在域外。只有范围是数字时才支持此方法。如果范围不是数字，则返回NaN

For a valid value *y* in the range, <i>continuous</i>(<i>continuous</i>.invert(<i>y</i>)) approximately equals *y*; similarly, for a valid value *x* in the domain, <i>continuous</i>.invert(<i>continuous</i>(<i>x</i>)) approximately equals *x*. The scale and its inverse may not be exact due to the limitations of floating point precision.

对于范围内的有效值y，连续（continuous .invert（y））近似等于y ; 类似地，对于域中的有效值x，连续 .invert（continuous（x））近似等于x。由于浮点精度的限制，规模及其反比可能不准确。

<a name="continuous_domain" href="#continuous_domain">#</a> <i>continuous</i>.<b>domain</b>([<i>domain</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/continuous.js#L92 "Source")

If *domain* is specified, sets the scale’s domain to the specified array of numbers. The array must contain two or more elements. If the elements in the given array are not numbers, they will be coerced to numbers. If *domain* is not specified, returns a copy of the scale’s current domain.

如果指定了域，则将比例域设置为指定的数字数组。该数组必须包含两个或更多个元素。如果给定数组中的元素不是数字，它们将被强制为数字。如果未指定域，则返回该比例的当前域的副本。

Although continuous scales typically have two values each in their domain and range, specifying more than two values produces a piecewise scale. For example, to create a diverging color scale that interpolates between white and red for negative values, and white and green for positive values, say:

虽然连续尺度在其域和范围中通常都有两个值，但指定两个以上的值会产生分段尺度。例如，要创建一个在白色和红色之间插值为负值的发散色彩比例，以及为正值插值白色和绿色，如下：

```js
var color = d3.scaleLinear()
    .domain([-1, 0, 1])
    .range(["red", "white", "green"]);

color(-0.5); // "rgb(255, 128, 128)"
color(+0.5); // "rgb(128, 192, 128)"
```

Internally, a piecewise scale performs a [binary search](https://github.com/d3/d3-array#bisect) for the range interpolator corresponding to the given domain value. Thus, the domain must be in ascending or descending order. If the domain and range have different lengths *N* and *M*, only the first *min(N,M)* elements in each are observed.

在内部，分段标度对与给定域值对应的范围内插器执行二分搜索。因此，域名必须按升序或降序排列。如果域和范围具有不同的长度N和M，则仅观察每个中的第一个最小（N，M）元素。

<a name="continuous_range" href="#continuous_range">#</a> <i>continuous</i>.<b>range</b>([<i>range</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/continuous.js#L96 "Source")

If *range* is specified, sets the scale’s range to the specified array of values. The array must contain two or more elements. Unlike the [domain](#continuous_domain), elements in the given array need not be numbers; any value that is supported by the underlying [interpolator](#continuous_interpolate) will work, though note that numeric ranges are required for [invert](#continuous_invert). If *range* is not specified, returns a copy of the scale’s current range. See [*continuous*.interpolate](#continuous_interpolate) for more examples.

如果指定范围，则将比例范围设置为指定的值数组。该数组必须包含两个或更多个元素。与域不同，给定数组中的元素不一定是数字; 底层插补器支持的任何值都可以使用，但请注意数值范围对于反转是必需的。如果未指定范围，则返回刻度的当前范围的副本。有关更多示例，请参阅连续插值。

<a name="continuous_rangeRound" href="#continuous_rangeRound">#</a> <i>continuous</i>.<b>rangeRound</b>([<i>range</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/continuous.js#L100 "Source")

Sets the scale’s [*range*](#continuous_range) to the specified array of values while also setting the scale’s [interpolator](#continuous_interpolate) to [interpolateRound](https://github.com/d3/d3-interpolate#interpolateRound). This is a convenience method equivalent to:

将刻度的范围设置为指定的数组值，同时将刻度的插值器设置为interpolateRound。这是简写，相当于：

```js
continuous
    .range(range)
    .interpolate(d3.interpolateRound);
```

The rounding interpolator is sometimes useful for avoiding antialiasing artifacts, though also consider the [shape-rendering](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/shape-rendering) “crispEdges” styles. Note that this interpolator can only be used with numeric ranges.

舍入插值器有时可用于避免抗锯齿伪像，但也可以考虑形状呈现 “crispEdges”样式。请注意，此插补器只能用于数字范围。

<a name="continuous_clamp" href="#continuous_clamp">#</a> <i>continuous</i>.<b>clamp</b>(<i>clamp</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/continuous.js#L104 "Source")

If *clamp* is specified, enables or disables clamping accordingly. If clamping is disabled and the scale is passed a value outside the [domain](#continuous_domain), the scale may return a value outside the [range](#continuous_range) through extrapolation. If clamping is enabled, the return value of the scale is always within the scale’s range. Clamping similarly applies to [*continuous*.invert](#continuous_invert). For example:

如果指定了钳位，则相应地启用或禁用钳位。如果钳位被禁用，并且规模被传递外部的值域，规模可能外侧返回一个值范围通过外推法。如果启用了钳位，秤的返回值始终在秤的范围内。钳位同样适用于连续的反转。例如：

```js
var x = d3.scaleLinear()
    .domain([10, 130])
    .range([0, 960]);

x(-10); // -160, outside range
x.invert(-160); // -10, outside domain

x.clamp(true);
x(-10); // 0, clamped to range
x.invert(-160); // 10, clamped to domain
```

If *clamp* is not specified, returns whether or not the scale currently clamps values to within the range.

如果未指定钳位，则返回当前标尺是否将值钳位在该范围内。

<a name="continuous_interpolate" href="#continuous_interpolate">#</a> <i>continuous</i>.<b>interpolate</b>(<i>interpolate</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/continuous.js#L108 "Source")

If *interpolate* is specified, sets the scale’s [range](#continuous_range) interpolator factory. This interpolator factory is used to create interpolators for each adjacent pair of values from the range; these interpolators then map a normalized domain parameter *t* in [0, 1] to the corresponding value in the range. If *factory* is not specified, returns the scale’s current interpolator factory, which defaults to [interpolate](https://github.com/d3/d3-interpolate#interpolate). See [d3-interpolate](https://github.com/d3/d3-interpolate) for more interpolators.

For example, consider a diverging color scale with three colors in the range:

如果插补指定，设置缩放范围内插器厂。该内插器工厂用于为该范围内的每个相邻值创建内插器; 这些内插器然后将[0，1]中的归一化的域参数t映射到该范围中的对应值。如果未指定工厂，则返回标尺的当前内插器工厂，该工厂默认为内插。有关更多内插器，请参阅d3- interpolate。
例如，考虑范围内具有三种颜色的发散色标：

```js
var color = d3.scaleLinear()
    .domain([-100, 0, +100])
    .range(["red", "white", "green"]);
```

Two interpolators are created internally by the scale, equivalent to:

两个内插器由内部按比例创建，相当于：

```js
var i0 = d3.interpolate("red", "white"),
    i1 = d3.interpolate("white", "green");
```

A common reason to specify a custom interpolator is to change the color space of interpolation. For example, to use [HCL](https://github.com/d3/d3-interpolate#interpolateHcl):

指定自定义插补器的常见原因是更改插值的颜色空间。例如，要使用HCL：

```js
var color = d3.scaleLinear()
    .domain([10, 100])
    .range(["brown", "steelblue"])
    .interpolate(d3.interpolateHcl);
```

Or for [Cubehelix](https://github.com/d3/d3-interpolate#interpolateCubehelix) with a custom gamma:

或者对于具有自定义伽玛的Cubehelix：

```js
var color = d3.scaleLinear()
    .domain([10, 100])
    .range(["brown", "steelblue"])
    .interpolate(d3.interpolateCubehelix.gamma(3));
```

Note: the [default interpolator](https://github.com/d3/d3-interpolate#interpolate) **may reuse return values**. For example, if the range values are objects, then the value interpolator always returns the same object, modifying it in-place. If the scale is used to set an attribute or style, this is typically acceptable (and desirable for performance); however, if you need to store the scale’s return value, you must specify your own interpolator or make a copy as appropriate.

注意：默认插补器 可能会重用返回值。例如，如果范围值是对象，则值内插器始终返回相同的对象，并在原地进行修改。如果使用比例来设置属性或样式，这通常是可以接受的（并且对于性能而言是可取的）; 但是，如果您需要存储比例的返回值，则必须指定自己的插补器或根据需要制作副本。

<a name="continuous_ticks" href="#continuous_ticks">#</a> <i>continuous</i>.<b>ticks</b>([<i>count</i>])

Returns approximately *count* representative values from the scale’s [domain](#continuous_domain). If *count* is not specified, it defaults to 10. The returned tick values are uniformly spaced, have human-readable values (such as multiples of powers of 10), and are guaranteed to be within the extent of the domain. Ticks are often used to display reference lines, or tick marks, in conjunction with the visualized data. The specified *count* is only a hint; the scale may return more or fewer values depending on the domain. See also d3-array’s [ticks](https://github.com/d3/d3-array#ticks).

返回约数从规模上的代表值域。如果未指定count，则默认为10.返回的刻度值是均匀间隔的，具有人类可读的值（例如10的幂的倍数），并且保证在该范围内。刻度通常用于显示参考线或刻度线，并与可视化数据结合使用。指定的计数只是一个提示; 规模可能会返回更多或更少的值，具体取决于域。另请参阅d3数组的刻度

<a name="continuous_tickFormat" href="#continuous_tickFormat">#</a> <i>continuous</i>.<b>tickFormat</b>([<i>count</i>[, <i>specifier</i>]]) [<>](https://github.com/d3/d3-scale/blob/master/src/tickFormat.js "Source")

Returns a [number format](https://github.com/d3/d3-format) function suitable for displaying a tick value, automatically computing the appropriate precision based on the fixed interval between tick values. The specified *count* should have the same value as the count that is used to generate the [tick values](#continuous_ticks).

返回适用于显示刻度值的数字格式函数，根据刻度值之间的固定间隔自动计算适当的精度。指定的计数值应与用于生成滴答值的计数值相同

An optional *specifier* allows a [custom format](https://github.com/d3/d3-format#locale_format) where the precision of the format is automatically set by the scale as appropriate for the tick interval. For example, to format percentage change, you might say:

一个可选的说明符允许自定义格式，其格式的精度可以根据刻度间隔的适当比例自动设置。例如，要格式化百分比变化，您可能会说：

```js
var x = d3.scaleLinear()
    .domain([-1, 1])
    .range([0, 960]);

var ticks = x.ticks(5),
    tickFormat = x.tickFormat(5, "+%");

ticks.map(tickFormat); // ["-100%", "-50%", "+0%", "+50%", "+100%"]
```

If *specifier* uses the format type `s`, the scale will return a [SI-prefix format](https://github.com/d3/d3-format#locale_formatPrefix) based on the largest value in the domain. If the *specifier* already specifies a precision, this method is equivalent to [*locale*.format](https://github.com/d3/d3-format#locale_format).

如果说明符使用格式类型s，则该比例将根据域中的最大值返回SI前缀格式。如果说明符已经指定了精度，则此方法等效于locale .format。

<a name="continuous_nice" href="#continuous_nice">#</a> <i>continuous</i>.<b>nice</b>([<i>count</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/nice.js "Source")

Extends the [domain](#continuous_domain) so that it starts and ends on nice round values. This method typically modifies the scale’s domain, and may only extend the bounds to the nearest round value. An optional tick *count* argument allows greater control over the step size used to extend the bounds, guaranteeing that the returned [ticks](#continuous_ticks) will exactly cover the domain. Nicing is useful if the domain is computed from data, say using [extent](https://github.com/d3/d3-array#extent), and may be irregular. For example, for a domain of [0.201479…, 0.996679…], a nice domain might be [0.2, 1.0]. If the domain has more than two values, nicing the domain only affects the first and last value. See also d3-array’s [tickStep](https://github.com/d3/d3-array#tickStep).

Nicing a scale only modifies the current domain; it does not automatically nice domains that are subsequently set using [*continuous*.domain](#continuous_domain). You must re-nice the scale after setting the new domain, if desired.


扩展域，使其开始并以不错的一轮值结束。此方法通常会修改比例的域，并且可能只会将边界扩展到最近的轮值。可选的滴答计数参数允许更好地控制用于扩展边界的步长，从而保证返回的滴答精确地覆盖该域。如果域是根据数据进行计算的，例如使用范围，并且可能不规则，则Nicing很有用。例如，对于[0.201479 ...，0.996679 ...]的域，一个很好的域可能是[0.2,1.0]。如果该域有两个以上的值，则禁止域仅影响第一个和最后一个值。另请参阅d3-array的tickStep。
缩小比例只会修改当前域; 它不会自动使用连续的 .domain进行设置。如果需要，您必须在设置新域后重新调整比例。

<a name="continuous_copy" href="#continuous_copy">#</a> <i>continuous</i>.<b>copy</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/continuous.js#L59 "Source")

Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.

返回此比例的精确副本。此比例的变化不会影响返回的比例，反之亦然。

#### Linear Scales

<a name="scaleLinear" href="#scaleLinear">#</a> d3.<b>scaleLinear</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/linear.js "Source")

Constructs a new [continuous scale](#continuous-scales) with the unit [domain](#continuous_domain) [0, 1], the unit [range](#continuous_range) [0, 1], the [default](https://github.com/d3/d3-interpolate#interpolate) [interpolator](#continuous_interpolate) and [clamping](#continuous_clamp) disabled. Linear scales are a good default choice for continuous quantitative data because they preserve proportional differences. Each range value *y* can be expressed as a function of the domain value *x*: *y* = *mx* + *b*.

用单位域 [0，1]，单位范围 [0,1]，默认插补器和禁用钳位构造一个新的连续标度。线性标度是连续定量数据的良好默认选择，因为它们保留了比例差异。每个范围值y可以表示为域值x的函数：y = mx + b。

#### Power Scales

Power scales are similar to [linear scales](#linear-scales), except an exponential transform is applied to the input domain value before the output range value is computed. Each range value *y* can be expressed as a function of the domain value *x*: *y* = *mx^k* + *b*, where *k* is the [exponent](#pow_exponent) value. Power scales also support negative domain values, in which case the input value and the resulting output value are multiplied by -1.

功率比例与线性比例相似，只是在计算输出范围值之前将指数变换应用于输入域值。每个范围值y可以表示为域值x的函数：y = mx ^ k + b，其中k是指数值。功率比例还支持负域值，在这种情况下，输入值和结果输出值将乘以-1

<a name="scalePow" href="#scalePow">#</a> d3.<b>scalePow</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/pow.js "Source")

Constructs a new [continuous scale](#continuous-scales) with the unit [domain](#continuous_domain) [0, 1], the unit [range](#continuous_range) [0, 1], the [exponent](#pow_exponent) 1, the [default](https://github.com/d3/d3-interpolate#interpolate) [interpolator](#continuous_interpolate) and [clamping](#continuous_clamp) disabled. (Note that this is effectively a [linear](#linear-scales) scale until you set a different exponent.)

用单位域 [0，1]，单位范围 [0,1]，指数 1，默认插补器和禁用钳位构造一个新的连续标度。（请注意，除非您设置不同的指数，否则这实际上是一个线性刻度。）

<a name="pow" href="#_pow">#</a> <i>pow</i>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/pow.js#L9 "Source")

See [*continuous*](#_continuous).

<a name="pow_invert" href="#pow_invert">#</a> <i>pow</i>.<b>invert</b>(<i>value</i>)

See [*continuous*.invert](#continuous_invert).

<a name="pow_exponent" href="#pow_exponent">#</a> <i>pow</i>.<b>exponent</b>([<i>exponent</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/pow.js#L25 "Source")

If *exponent* is specified, sets the current exponent to the given numeric value. If *exponent* is not specified, returns the current exponent, which defaults to 1. (Note that this is effectively a [linear](#linear-scales) scale until you set a different exponent.)

如果指数指定，将当前指数给定的数字值。如果未指定指数，则返回当前指数，该指数默认为1.（请注意，除非设置不同的指数，否则这实际上是一个线性比例。）

<a name="pow_domain" href="#pow_domain">#</a> <i>pow</i>.<b>domain</b>([<i>domain</i>])

See [*continuous*.domain](#continuous_domain).

<a name="pow_range" href="#pow_range">#</a> <i>pow</i>.<b>range</b>([<i>range</i>])

See [*continuous*.range](#continuous_range).

<a name="pow_rangeRound" href="#pow_rangeRound">#</a> <i>pow</i>.<b>rangeRound</b>([<i>range</i>])

See [*continuous*.rangeRound](#continuous_rangeRound).

<a name="pow_clamp" href="#pow_clamp">#</a> <i>pow</i>.<b>clamp</b>(<i>clamp</i>)

See [*continuous*.clamp](#continuous_clamp).

<a name="pow_interpolate" href="#pow_interpolate">#</a> <i>pow</i>.<b>interpolate</b>(<i>interpolate</i>)

See [*continuous*.interpolate](#continuous_interpolate).

<a name="pow_ticks" href="#pow_ticks">#</a> <i>pow</i>.<b>ticks</b>([<i>count</i>])

See [*continuous*.ticks](#continuous_ticks).

<a name="pow_tickFormat" href="#pow_tickFormat">#</a> <i>pow</i>.<b>tickFormat</b>([<i>count</i>[, <i>specifier</i>]])

See [*continuous*.tickFormat](#continuous_tickFormat).

<a name="pow_nice" href="#pow_nice">#</a> <i>pow</i>.<b>nice</b>([<i>count</i>])

See [*continuous*.nice](#continuous_nice).

<a name="pow_copy" href="#pow_copy">#</a> <i>pow</i>.<b>copy</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/pow.js#L29 "Source")

See [*continuous*.copy](#continuous_copy).

<a name="scaleSqrt" href="#scaleSqrt">#</a> d3.<b>scaleSqrt</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/pow.js#L36 "Source")

Constructs a new [continuous](#continuous-scales) [power scale](#power-scales) with the unit [domain](#continuous_domain) [0, 1], the unit [range](#continuous_range) [0, 1], the [exponent](#pow_exponent) 0.5, the [default](https://github.com/d3/d3-interpolate#interpolate) [interpolator](#continuous_interpolate) and [clamping](#continuous_clamp) disabled. This is a convenience method equivalent to

 使用单位域 [0，1]，单位范围 [0,1]，指数 0.5，默认插补器和禁用钳位构造新的连续 功率标度。这是相当于简写的方法。
 
 `d3.scalePow().exponent(0.5)`.

#### Log Scales

Log scales are similar to [linear scales](#linear-scales), except a logarithmic transform is applied to the input domain value before the output range value is computed. The mapping to the range value *y* can be expressed as a function of the domain value *x*: *y* = *m* log(<i>x</i>) + *b*.

As log(0) = -∞, a log scale domain must be **strictly-positive or strictly-negative**; the domain must not include or cross zero. A log scale with a positive domain has a well-defined behavior for positive values, and a log scale with a negative domain has a well-defined behavior for negative values. (For a negative domain, input and output values are implicitly multiplied by -1.) The behavior of the scale is undefined if you pass a negative value to a log scale with a positive domain or vice versa.

对数尺度类似于线性尺度，除了在计算输出范围值之前将对数变换应用于输入域值。映射到范围值y可以表示为域值x的函数：y = m log（x）+ b。

由于log（0）=-∞，对数标度域必须严格为正或严格为负 ; 该域不得包含或交叉为零。具有正域的对数标度具有定义良好的正值的行为，具有负域的对数标度具有定义良好的负值的行为。（对于负域，输入和输出值隐式乘以-1）。如果将负值传递给具有正域的对数刻度，反之亦然，则刻度的行为不确定。

<a name="scaleLog" href="#scaleLog">#</a> d3.<b>scaleLog</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/log.js "Source")

Constructs a new [continuous scale](#continuous-scales) with the [domain](#log_domain) [1, 10], the unit [range](#log_range) [0, 1], the [base](#log_base) 10, the [default](https://github.com/d3/d3-interpolate#interpolate) [interpolator](#log_interpolate) and [clamping](#log_clamp) disabled.

使用域 [1，10]，单位范围 [0,1]，基数 10，默认插补器和禁用钳位构造新的连续标度。

<a name="log" href="#_log">#</a> <i>log</i>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/log.js#L42 "Source")

See [*continuous*](#_continuous).

<a name="log_invert" href="#log_invert">#</a> <i>log</i>.<b>invert</b>(<i>value</i>)

See [*continuous*.invert](#continuous_invert).

<a name="log_base" href="#log_base">#</a> <i>log</i>.<b>base</b>([<i>base</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/log.js#L55 "Source")

If *base* is specified, sets the base for this logarithmic scale to the specified value. If *base* is not specified, returns the current base, which defaults to 10.

如果base指定，设置此对数标度为指定值的基础。如果未指定base，则返回当前的基数，默认值为10

<a name="log_domain" href="#log_domain">#</a> <i>log</i>.<b>domain</b>([<i>domain</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/log.js#L59 "Source")

See [*continuous*.domain](#continuous_domain).

<a name="log_range" href="#log_range">#</a> <i>log</i>.<b>range</b>([<i>range</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/continuous.js#L96 "Source")

See [*continuous*.range](#continuous_range).

<a name="log_rangeRound" href="#log_rangeRound">#</a> <i>log</i>.<b>rangeRound</b>([<i>range</i>])

See [*continuous*.rangeRound](#continuous_rangeRound).

<a name="log_clamp" href="#log_clamp">#</a> <i>log</i>.<b>clamp</b>(<i>clamp</i>)

See [*continuous*.clamp](#continuous_clamp).

<a name="log_interpolate" href="#log_interpolate">#</a> <i>log</i>.<b>interpolate</b>(<i>interpolate</i>)

See [*continuous*.interpolate](#continuous_interpolate).

<a name="log_ticks" href="#log_ticks">#</a> <i>log</i>.<b>ticks</b>([<i>count</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/log.js#L63 "Source")

Like [*continuous*.ticks](#continuous_ticks), but customized for a log scale. If the [base](#log_base) is an integer, the returned ticks are uniformly spaced within each integer power of base; otherwise, one tick per power of base is returned. The returned ticks are guaranteed to be within the extent of the domain. If the orders of magnitude in the [domain](#log_domain) is greater than *count*, then at most one tick per power is returned. Otherwise, the tick values are unfiltered, but note that you can use [*log*.tickFormat](#log_tickFormat) to filter the display of tick labels. If *count* is not specified, it defaults to 10.

像continuous.ticks一样，但是这是为log scale定制。如果基数是整数，则返回的刻度在基数的每个整数次幂内均匀间隔; 否则，返回每个基数的一个勾号。返回的刻度保证在域的范围内。如果域中的数量级大于count，则每个power最多返回一个tick。否则，标记值未经过滤，但请注意，您可以使用log .tickFormat来过滤刻度标签的显示。如果未指定count，则默认为10。

<a name="log_tickFormat" href="#log_tickFormat">#</a> <i>log</i>.<b>tickFormat</b>([<i>count</i>[, <i>specifier</i>]]) [<>](https://github.com/d3/d3-scale/blob/master/src/log.js#L103 "Source")

Like [*continuous*.tickFormat](#continuous_tickFormat), but customized for a log scale. The specified *count* typically has the same value as the count that is used to generate the [tick values](#continuous_ticks). If there are too many ticks, the formatter may return the empty string for some of the tick labels; however, note that the ticks are still shown. To disable filtering, specify a *count* of Infinity. When specifying a count, you may also provide a format *specifier* or format function. For example, to get a tick formatter that will display 20 ticks of a currency, say `log.tickFormat(20, "$,f")`. If the specifier does not have a defined precision, the precision will be set automatically by the scale, returning the appropriate format. This provides a convenient way of specifying a format whose precision will be automatically set by the scale.

像continuous.tickFormat一样，但是这是为log scale定制。指定的计数通常与用于生成刻度值的计数值相同。如果记号太多，格式化程序可能会返回一些空格字符串作为标记; 但是请注意，tick仍然显示。要禁用过滤，请指定Infinity 的计数。指定计数时，您还可以提供格式说明符或格式函数。例如，要获得一个将显示20个货币的滴答的格式化程序，例如log.tickFormat(20, "$,f")。如果说明符不具有定义的精度，则精度将由比例自动设置，返回适当的格式。这提供了一种指定格式的便捷方法，其精度将由比例自动设置。

<a name="log_nice" href="#log_nice">#</a> <i>log</i>.<b>nice</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/log.js#L116 "Source")

Like [*continuous*.nice](#continuous_nice), except extends the domain to integer powers of [base](#log_base). For example, for a domain of [0.201479…, 0.996679…], and base 10, the nice domain is [0.1, 1]. If the domain has more than two values, nicing the domain only affects the first and last value.

像continuous.nice一样，除了将域扩展为基数的整数次幂。例如，对于[0.201479 ...，0.996679 ...]和基数10的域，nice域是[0.1,1]。如果该域有两个以上的值，则禁止域仅影响第一个和最后一个值

<a name="log_copy" href="#log_copy">#</a> <i>log</i>.<b>copy</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/log.js#L123 "Source")

See [*continuous*.copy](#continuous_copy).

#### Identity Scales

Identity scales are a special case of [linear scales](#linear-scales) where the domain and range are identical; the scale and its invert method are thus the identity function. These scales are occasionally useful when working with pixel coordinates, say in conjunction with an axis or brush. Identity scales do not support [rangeRound](#continuous_rangeRound), [clamp](#continuous_clamp) or [interpolate](#continuous_interpolate).

Identity scales是域和范围相同的线性尺度的特例; 因此尺度及其反演方法是标识函数。当使用像素坐标时，这些缩放比例偶尔是有用的，比如与轴或画笔结合使用。Identity scales不支持rangeRound，clamp或interpolate。

<a name="scaleIdentity" href="#scaleIdentity">#</a> d3.<b>scaleIdentity</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/identity.js "Source")

Constructs a new identity scale with the unit [domain](#continuous_domain) [0, 1] and the unit [range](#continuous_range) [0, 1].

#### Time Scales

Time scales are a variant of [linear scales](#linear-scales) that have a temporal domain: domain values are coerced to [dates](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Date) rather than numbers, and [invert](#continuous_invert) likewise returns a date. Time scales implement [ticks](#time_ticks) based on [calendar intervals](https://github.com/d3/d3-time), taking the pain out of generating axes for temporal domains.

For example, to create a position encoding:

时间尺度是具有时间域的线性尺度的变体：域值强制为日期而不是数字，反转同样返回日期。时间刻度根据日历时间间隔实施刻度，从时间域的生成轴中消除痛苦。

例如，要创建位置编码：

```js
var x = d3.scaleTime()
    .domain([new Date(2000, 0, 1), new Date(2000, 0, 2)])
    .range([0, 960]);

x(new Date(2000, 0, 1,  5)); // 200
x(new Date(2000, 0, 1, 16)); // 640
x.invert(200); // Sat Jan 01 2000 05:00:00 GMT-0800 (PST)
x.invert(640); // Sat Jan 01 2000 16:00:00 GMT-0800 (PST)
```

For a valid value *y* in the range, <i>time</i>(<i>time</i>.invert(<i>y</i>)) equals *y*; similarly, for a valid value *x* in the domain, <i>time</i>.invert(<i>time</i>(<i>x</i>)) equals *x*. The invert method is useful for interaction, say to determine the value in the domain that corresponds to the pixel location under the mouse.

对于范围内的有效值y，时间（时间 .invert（y））等于y ; 同样，对于域中的有效值x，时间 .invert（time（x））等于x。倒置方法对于交互非常有用，比如确定与鼠标下像素位置相对应的域中的值。

<a name="scaleTime" href="#scaleTime">#</a> d3.<b>scaleTime</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/time.js "Source")

Constructs a new time scale with the [domain](#time_domain) [2000-01-01, 2000-01-02], the unit [range](#time_range) [0, 1], the [default](https://github.com/d3/d3-interpolate#interpolate) [interpolator](#time_interpolate) and [clamping](#time_clamp) disabled.

使用域 [2000-01-01,2000-01-02] 构造一个新的时标，单位范围 [0,1]，默认 插补器和禁用钳位。

<a name="time" href="#_time">#</a> <i>time</i>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/time.js#L133 "Source")

See [*continuous*](#_continuous).

<a name="time_invert" href="#time_invert">#</a> <i>time</i>.<b>invert</b>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/time.js#L95 "Source")

See [*continuous*.invert](#continuous_invert).

<a name="time_domain" href="#time_domain">#</a> <i>time</i>.<b>domain</b>([<i>domain</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/time.js#L99 "Source")

See [*continuous*.domain](#continuous_domain).

<a name="time_range" href="#time_range">#</a> <i>time</i>.<b>range</b>([<i>range</i>])

See [*continuous*.range](#continuous_range).

<a name="time_rangeRound" href="#time_rangeRound">#</a> <i>time</i>.<b>rangeRound</b>([<i>range</i>])

See [*continuous*.rangeRound](#continuous_rangeRound).

<a name="time_clamp" href="#time_clamp">#</a> <i>time</i>.<b>clamp</b>(<i>clamp</i>)

See [*continuous*.clamp](#continuous_clamp).

<a name="time_interpolate" href="#time_interpolate">#</a> <i>time</i>.<b>interpolate</b>(<i>interpolate</i>)

See [*continuous*.interpolate](#continuous_interpolate).

<a name="time_ticks" href="#time_ticks">#</a> <i>time</i>.<b>ticks</b>([<i>count</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/time.js#L103 "Source")
<br><a name="time_ticks" href="#time_ticks">#</a> <i>time</i>.<b>ticks</b>([<i>interval</i>])

Returns representative dates from the scale’s [domain](#time_domain). The returned tick values are uniformly-spaced (mostly), have sensible values (such as every day at midnight), and are guaranteed to be within the extent of the domain. Ticks are often used to display reference lines, or tick marks, in conjunction with the visualized data.

An optional *count* may be specified to affect how many ticks are generated. If *count* is not specified, it defaults to 10. The specified *count* is only a hint; the scale may return more or fewer values depending on the domain. For example, to create ten default ticks, say:

从比例域返回代表性日期。返回的刻度值是均匀间隔的（大部分），具有合理的值（例如每天午夜），并且保证位于域的范围内。刻度通常用于显示参考线或刻度线，并与可视化数据结合使用。

可以指定可选的计数以影响生成的滴答数。如果未指定count，则默认为10.指定的计数仅为提示; 规模可能会返回更多或更少的值，具体取决于域。例如，要创建十个默认滴答，如下：

```js
var x = d3.scaleTime();

x.ticks(10);
// [Sat Jan 01 2000 00:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 03:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 06:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 09:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 12:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 15:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 18:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 21:00:00 GMT-0800 (PST),
//  Sun Jan 02 2000 00:00:00 GMT-0800 (PST)]
```

The following time intervals are considered for automatic ticks:

以下时间间隔被认为是自动滴答：

* 1-, 5-, 15- and 30-second.
* 1-, 5-, 15- and 30-minute.
* 1-, 3-, 6- and 12-hour.
* 1- and 2-day.
* 1-week.
* 1- and 3-month.
* 1-year.

In lieu of a *count*, a [time *interval*](https://github.com/d3/d3-time#intervals) may be explicitly specified. To prune the generated ticks for a given time *interval*, use [*interval*.every](https://github.com/d3/d3-time#interval_every). For example, to generate ticks at 15-[minute](https://github.com/d3/d3-time#minute) intervals:

代替计数，可以明确指定时间间隔。要修剪给定时间间隔内生成的滴答，请使用间隔 .every。例如，要以15 分钟的间隔生成滴答：

```js
var x = d3.scaleTime()
    .domain([new Date(2000, 0, 1, 0), new Date(2000, 0, 1, 2)]);

x.ticks(d3.timeMinute.every(15));
// [Sat Jan 01 2000 00:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 00:15:00 GMT-0800 (PST),
//  Sat Jan 01 2000 00:30:00 GMT-0800 (PST),
//  Sat Jan 01 2000 00:45:00 GMT-0800 (PST),
//  Sat Jan 01 2000 01:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 01:15:00 GMT-0800 (PST),
//  Sat Jan 01 2000 01:30:00 GMT-0800 (PST),
//  Sat Jan 01 2000 01:45:00 GMT-0800 (PST),
//  Sat Jan 01 2000 02:00:00 GMT-0800 (PST)]
```

Alternatively, pass a test function to [*interval*.filter](https://github.com/d3/d3-time#interval_filter):

或者，将测试函数传递给interval .filter：

```js
x.ticks(d3.timeMinute.filter(function(d) {
  return d.getMinutes() % 15 === 0;
}));
```

Note: in some cases, such as with day ticks, specifying a *step* can result in irregular spacing of ticks because time intervals have varying length.

注意：在某些情况下，例如使用星期标记，指定一个步骤可能会导致标记间隔不规则，因为时间间隔的长度不同

<a name="time_tickFormat" href="#time_tickFormat">#</a> <i>time</i>.<b>tickFormat</b>([<i>count</i>[, <i>specifier</i>]]) [<>](https://github.com/d3/d3-scale/blob/master/src/time.js#L115 "Source")
<br><a href="#time_tickFormat">#</a> <i>time</i>.<b>tickFormat</b>([<i>interval</i>[, <i>specifier</i>]])

Returns a time format function suitable for displaying [tick](#time_ticks) values. The specified *count* or *interval* is currently ignored, but is accepted for consistency with other scales such as [*continuous*.tickFormat](#continuous_tickFormat). If a format *specifier* is specified, this method is equivalent to [format](https://github.com/d3/d3-time-format#format). If *specifier* is not specified, the default time format is returned. The default multi-scale time format chooses a human-readable representation based on the specified date as follows:

返回适合显示刻度值的时间格式函数。指定的计数或时间间隔目前被忽略，但为了与其他尺度保持一致，continuous.tickFormat被接受。如果指定了格式说明符，则此方法与格式相同。如果符未指定，则返回默认的时间格式。默认多尺度时间格式根据指定的日期选择一个人类可读的表示，如下所示：

* `%Y` - for year boundaries, such as `2011`.
* `%B` - for month boundaries, such as `February`.
* `%b %d` - for week boundaries, such as `Feb 06`.
* `%a %d` - for day boundaries, such as `Mon 07`.
* `%I %p` - for hour boundaries, such as `01 AM`.
* `%I:%M` - for minute boundaries, such as `01:23`.
* `:%S` - for second boundaries, such as `:45`.
* `.%L` - milliseconds for all other times, such as `.012`.

Although somewhat unusual, this default behavior has the benefit of providing both local and global context: for example, formatting a sequence of ticks as [11 PM, Mon 07, 01 AM] reveals information about hours, dates, and day simultaneously, rather than just the hours [11 PM, 12 AM, 01 AM]. See [d3-time-format](https://github.com/d3/d3-time-format) if you’d like to roll your own conditional time format.

虽然有点不同寻常，但这种默认行为有利于提供本地和全局上下文：例如，[11 PM，Mon 07，01 AM]同时显示有关小时，日期和日期的信息，而不是格式化一系列刻度只是时间[下午11点，上午12点，上午01点]。如果您想推出自己的条件时间格式，请参阅d3-time- format。


<a name="time_nice" href="#time_nice">#</a> <i>time</i>.<b>nice</b>([<i>count</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/time.js#L119 "Source")
<br><a name="time_nice" href="#time_nice">#</a> <i>time</i>.<b>nice</b>([<i>interval</i>[, <i>step</i>]])

Extends the [domain](#time_domain) so that it starts and ends on nice round values. This method typically modifies the scale’s domain, and may only extend the bounds to the nearest round value. See [*continuous*.nice](#continuous_nice) for more.

An optional tick *count* argument allows greater control over the step size used to extend the bounds, guaranteeing that the returned [ticks](#time_ticks) will exactly cover the domain. Alternatively, a [time *interval*](https://github.com/d3/d3-time#intervals) may be specified to explicitly set the ticks. If an *interval* is specified, an optional *step* may also be specified to skip some ticks. For example, `time.nice(d3.timeSecond, 10)` will extend the domain to an even ten seconds (0, 10, 20, <i>etc.</i>). See [*time*.ticks](#time_ticks) and [*interval*.every](https://github.com/d3/d3-time#interval_every) for further detail.

Nicing is useful if the domain is computed from data, say using [extent](https://github.com/d3/d3-array#extent), and may be irregular. For example, for a domain of [2009-07-13T00:02, 2009-07-13T23:48], the nice domain is [2009-07-13, 2009-07-14]. If the domain has more than two values, nicing the domain only affects the first and last value.

扩展域，使其开始并以nice round值结束。此方法通常会修改比例的域，并且可能只会将边界扩展到最近的轮值。有关更多信息，请参见continuous.nice。

可选的滴答计数参数允许更好地控制用于扩展边界的步长，从而保证返回的滴答精确地覆盖该域。或者，可以指定时间间隔来明确设置滴答。如果指定了时间间隔，则还可以指定一个可选步骤来跳过一些滴答声。例如，time.nice(d3.timeSecond, 10)将域扩展到10秒（0,10,20 等）。请参阅time .ticks和interval .every以获取更多详细信息。

如果域是根据数据进行计算的，例如使用范围，并且可能不规则，则Nicing很有用。例如，对于[2009-07-13T00：02，2009-07-13T23：48]的域，nice域名为[2009-07-13，2009-07-14]。如果该域有两个以上的值，则禁止域仅影响第一个和最后一个值。

<a name="scaleUtc" href="#scaleUtc">#</a> d3.<b>scaleUtc</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/utcTime.js "Source")

Equivalent to [time](#time), but the returned time scale operates in [Coordinated Universal Time](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) rather than local time.

相当于时间，但返回的时间范围以协调世界时而不是当地时间运行。

### Sequential Scales

Sequential scales are similar to [continuous scales](#continuous-scales) in that they map a continuous, numeric input domain to a continuous output range. However, unlike continuous scales, the output range of a sequential scale is fixed by its interpolator and not configurable. These scales do not expose [invert](#continuous_invert), [range](#continuous_range), [rangeRound](#continuous_rangeRound) and [interpolate](#continuous_interpolate) methods.

Sequential scales类似于continuous scales，因为它们将连续的数字输入域映射到连续的输出范围。但是，与连续标度不同，顺序标度的输出范围由插补器固定，不可配置。这些比例尺不会显示反转，范围，rangeRound和插值方法。

<a name="scaleSequential" href="#scaleSequential">#</a> d3.<b>scaleSequential</b>(<i>interpolator</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/sequential.js "Source")

Constructs a new sequential scale with the given [*interpolator*](#sequential_interpolator) function. When the scale is [applied](#_sequential), the interpolator will be invoked with a value typically in the range [0, 1], where 0 represents the start of the domain, and 1 represents the end of the domain. For example, to implement the ill-advised [HSL](https://github.com/d3/d3-color#hsl) rainbow scale:

使用给定的插补函数构造一个新的顺序标度。当应用缩放比例时，将使用通常在[0，1]范围内的值来调用插值器，其中0代表域的起始位置，1代表域的末尾。例如，要实施不明智的HSL彩虹色标：

```js
var rainbow = d3.scaleSequential(function(t) {
  return d3.hsl(t * 360, 1, 0.5) + "";
});
```

A more aesthetically-pleasing and perceptually-effective cyclical hue encoding is to use [d3.interpolateRainbow](https://github.com/d3/d3-scale-chromatic/blob/master/README.md#interpolateRainbow):

更美观和感知有效的循环色调编码是使用d3.interpolateRainbow：

```js
var rainbow = d3.scaleSequential(d3.interpolateRainbow);
```

<a name="_sequential" href="#_sequential">#</a> <i>sequential</i>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/sequential.js#L3 "Source")

See [*continuous*](#_continuous).

<a name="sequential_domain" href="#sequential_domain">#</a> <i>sequential</i>.<b>domain</b>([<i>domain</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/sequential.js#L13 "Source")

See [*continuous*.domain](#continuous_domain). Note that a sequential scale’s domain must be numeric and must contain exactly two values.

请参阅连续的 .domain。请注意，顺序比例的域必须是数字，并且必须包含两个值。

<a name="sequential_clamp" href="#sequential_clamp">#</a> <i>sequential</i>.<b>clamp</b>([<i>clamp</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/sequential.js#L17 "Source")

See [*continuous*.clamp](#continuous_clamp).

<a name="sequential_interpolator" href="#sequential_interpolator">#</a> <i>sequential</i>.<b>interpolator</b>([<i>interpolator</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/sequential.js#L21 "Source")

If *interpolator* is specified, sets the scale’s interpolator to the specified function. If *interpolator* is not specified, returns the scale’s current interpolator.

如果指定了插补器，则将标尺的插补器设置为指定的函数。如果未指定插补器，则返回标尺的当前插补器。

<a name="sequential_copy" href="#sequential_copy">#</a> <i>sequential</i>.<b>copy</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/sequential.js#L25 "Source")

See [*continuous*.copy](#continuous_copy).

### Quantize Scales

Quantize scales are similar to [linear scales](#linear-scales), except they use a discrete rather than continuous range. The continuous input domain is divided into uniform segments based on the number of values in (*i.e.*, the cardinality of) the output range. Each range value *y* can be expressed as a quantized linear function of the domain value *x*: *y* = *m round(x)* + *b*. See [bl.ocks.org/4060606](http://bl.ocks.org/mbostock/4060606) for an example.

量化尺度与线性尺度相似，除了它们使用离散而非连续的范围。连续输入域根据输出范围中的值（即基数）的数量分成统一的段。每个范围值y可以表示为域值x的量化的线性函数：y = m round（x） + b。以bl.ocks.org/4060606为例。

<a name="scaleQuantize" href="#scaleQuantize">#</a> d3.<b>scaleQuantize</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/quantize.js "Source")

Constructs a new quantize scale with the unit [domain](#quantize_domain) [0, 1] and the unit [range](#quantize_range) [0, 1]. Thus, the default quantize scale is equivalent to the [Math.round](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Math/round) function.

用单位域 [0，1]和单位范围 [0，1 ] 构造新的量化比例。因此，默认的量化比例等于Math.round函数。

<a name="_quantize" href="#_quantize">#</a> <i>quantize</i>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/quantize.js#L5 "Source")

Given a *value* in the input [domain](#quantize_domain), returns the corresponding value in the output [range](#quantize_range). For example, to apply a color encoding:

给定输入域中的值，返回输出范围中的对应值。例如，要应用颜色编码：

```js
var color = d3.scaleQuantize()
    .domain([0, 1])
    .range(["brown", "steelblue"]);

color(0.49); // "brown"
color(0.51); // "steelblue"
```

Or dividing the domain into three equally-sized parts with different range values to compute an appropriate stroke width:

或者将域分成三个具有不同范围值的大小相等的部分来计算适当的笔画宽度：

```js
var width = d3.scaleQuantize()
    .domain([10, 100])
    .range([1, 2, 4]);

width(20); // 1
width(50); // 2
width(80); // 4
```

<a name="quantize_invertExtent" href="#quantize_invertExtent">#</a> <i>quantize</i>.<b>invertExtent</b>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/quantize.js#L31 "Source")

Returns the extent of values in the [domain](#quantize_domain) [<i>x0</i>, <i>x1</i>] for the corresponding *value* in the [range](#quantize_range): the inverse of [*quantize*](#_quantize). This method is useful for interaction, say to determine the value in the domain that corresponds to the pixel location under the mouse.

如果指定了域，则将比例尺的域设置为指定的两个元素的数字数组。如果给定数组中的元素不是数字，它们将被强制为数字。如果未指定域，则返回比例尺的当前域

```js
var width = d3.scaleQuantize()
    .domain([10, 100])
    .range([1, 2, 4]);

width.invertExtent(2); // [40, 70]
```

<a name="quantize_domain" href="#quantize_domain">#</a> <i>quantize</i>.<b>domain</b>([<i>domain</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/quantize.js#L23 "Source")

If *domain* is specified, sets the scale’s domain to the specified two-element array of numbers. If the elements in the given array are not numbers, they will be coerced to numbers. If *domain* is not specified, returns the scale’s current domain.

如果指定了域，则将比例尺的域设置为指定的两个元素的数字数组。如果给定数组中的元素不是数字，它们将被强制为数字。如果未指定域，则返回比例尺的当前域。

<a name="quantize_range" href="#quantize_range">#</a> <i>quantize</i>.<b>range</b>([<i>range</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/quantize.js#L27 "Source")

If *range* is specified, sets the scale’s range to the specified array of values. The array may contain any number of discrete values. The elements in the given array need not be numbers; any value or type will work. If *range* is not specified, returns the scale’s current range.

如果指定范围，则将比例范围设置为指定的值数组。该数组可能包含任意数量的离散值。给定数组中的元素不一定是数字; 任何价值或类型将工作。如果未指定范围，则返回比例的当前范围。

<a name="quantize_ticks" href="#quantize_ticks">#</a> <i>quantize</i>.<b>ticks</b>([<i>count</i>])

Equivalent to [*continuous*.ticks](#continuous_ticks).

<a name="quantize_tickFormat" href="#quantize_tickFormat">#</a> <i>quantize</i>.<b>tickFormat</b>([<i>count</i>[, <i>specifier</i>]]) [<>](https://github.com/d3/d3-scale/blob/master/src/linear.js#L14 "Source")

Equivalent to [*continuous*.tickFormat](#continuous_tickFormat).

<a name="quantize_nice" href="#quantize_nice">#</a> <i>quantize</i>.<b>nice</b>()

Equivalent to [*continuous*.nice](#continuous_nice).

<a name="quantize_copy" href="#quantize_copy">#</a> <i>quantize</i>.<b>copy</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/quantize.js#L39 "Source")

Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.

返回此比例的精确副本。此比例的变化不会影响返回的比例，反之亦然。

### Quantile Scales

Quantile scales map a sampled input domain to a discrete range. The domain is considered continuous and thus the scale will accept any reasonable input value; however, the domain is specified as a discrete set of sample values. The number of values in (the cardinality of) the output range determines the number of quantiles that will be computed from the domain. To compute the quantiles, the domain is sorted, and treated as a [population of discrete values](https://en.wikipedia.org/wiki/Quantile#Quantiles_of_a_population); see d3-array’s [quantile](https://github.com/d3/d3-array#quantile). See [bl.ocks.org/8ca036b3505121279daf](http://bl.ocks.org/mbostock/8ca036b3505121279daf) for an example.

分位量表将采样的输入域映射到离散范围。该域被认为是连续的，因此该比例将接受任何合理的输入值; 然而，该域被指定为离散的一组样本值。输出范围（的基数）中的值的数量决定了将从域计算的分位数的数量。为了计算分位数，将该域进行排序，并将其视为离散值的总体 ; 请参阅d3-array的分位数。以bl.ocks.org/8ca036b3505121279daf为例。

<a name="scaleQuantile" href="#scaleQuantile">#</a> d3.<b>scaleQuantile</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/quantile.js "Source")

Constructs a new quantile scale with an empty [domain](#quantile_domain) and an empty [range](#quantile_range). The quantile scale is invalid until both a domain and range are specified.

用空域和空范围构造一个新的分位数标度。在指定域和范围之前，分位数比例无效。

<a name="_quantile" href="#_quantile">#</a> <i>quantile</i>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/quantile.js#L4 "Source")

Given a *value* in the input [domain](#quantile_domain), returns the corresponding value in the output [range](#quantile_range).

给定输入域中的值，返回输出范围中的对应值。

<a name="quantile_invertExtent" href="#quantile_invertExtent">#</a> <i>quantile</i>.<b>invertExtent</b>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/quantile.js#L20 "Source")

Returns the extent of values in the [domain](#quantile_domain) [<i>x0</i>, <i>x1</i>] for the corresponding *value* in the [range](#quantile_range): the inverse of [*quantile*](#_quantile). This method is useful for interaction, say to determine the value in the domain that corresponds to the pixel location under the mouse.

返回范围中相应值的域 [ x0，x1 ]中值的范围：分位数的倒数。这种方法对于交互很有用，比方说确定域中与鼠标下像素位置相对应的值。

<a name="quantile_domain" href="#quantile_domain">#</a> <i>quantile</i>.<b>domain</b>([<i>domain</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/quantile.js#L28 "Source")

If *domain* is specified, sets the domain of the quantile scale to the specified set of discrete numeric values. The array must not be empty, and must contain at least one numeric value; NaN, null and undefined values are ignored and not considered part of the sample population. If the elements in the given array are not numbers, they will be coerced to numbers. A copy of the input array is sorted and stored internally. If *domain* is not specified, returns the scale’s current domain.

如果域指定，设定位数规模到指定的组离散数值的域。该数组不能为空，并且必须包含至少一个数值; NaN，空值和未定义值被忽略，不被视为样本总体的一部分。如果给定数组中的元素不是数字，它们将被强制为数字。输入数组的副本将在内部排序并存储。如果未指定域，则返回比例尺的当前域。

<a name="quantile_range" href="#quantile_range">#</a> <i>quantile</i>.<b>range</b>([<i>range</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/quantile.js#L36 "Source")

If *range* is specified, sets the discrete values in the range. The array must not be empty, and may contain any type of value. The number of values in (the cardinality, or length, of) the *range* array determines the number of quantiles that are computed. For example, to compute quartiles, *range* must be an array of four elements such as [0, 1, 2, 3]. If *range* is not specified, returns the current range.

如果指定范围，则将离散值设置在范围内。该数组不能为空，并且可能包含任何类型的值。范围数组中的（基数或长度）值的数量决定了计算出的分位数。例如，要计算四分位数，范围必须是由四个元素组成的数组，例如[0,1,2,3]。如果未指定范围，则返回当前范围。

<a name="quantile_quantiles" href="#quantile_quantiles">#</a> <i>quantile</i>.<b>quantiles</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/quantile.js#L40 "Source")

Returns the quantile thresholds. If the [range](#quantile_range) contains *n* discrete values, the returned array will contain *n* - 1 thresholds. Values less than the first threshold are considered in the first quantile; values greater than or equal to the first threshold but less than the second threshold are in the second quantile, and so on. Internally, the thresholds array is used with [bisect](https://github.com/d3/d3-array#bisect) to find the output quantile associated with the given input value.

返回分位数阈值。如果范围包含n个离散值，则返回的数组将包含n - 1个阈值。在第一分位数中考虑小于第一阈值的值; 大于或等于第一阈值但小于第二阈值的值在第二分位数中，等等。在内部，阈值数组用于平分以查找与给定输入值关联的输出分位数。

<a name="quantile_copy" href="#quantile_copy">#</a> <i>quantile</i>.<b>copy</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/quantile.js#L44 "Source")

Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.

返回此比例的精确副本。此比例的变化不会影响返回的比例，反之亦然。

### Threshold Scales

Threshold scales are similar to [quantize scales](#quantize-scales), except they allow you to map arbitrary subsets of the domain to discrete values in the range. The input domain is still continuous, and divided into slices based on a set of threshold values. See [bl.ocks.org/3306362](http://bl.ocks.org/mbostock/3306362) for an example.

阈值比例与量化比例相似，只不过它们允许您将域的任意子集映射到范围中的离散值。输入域仍然是连续的，并根据一组阈值划分成片。以bl.ocks.org/3306362为例。

<a name="scaleThreshold" href="#scaleThreshold">#</a> d3.<b>scaleThreshold</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/threshold.js "Source")

Constructs a new threshold scale with the default [domain](#threshold_domain) [0.5] and the default [range](#threshold_range) [0, 1]. Thus, the default threshold scale is equivalent to the [Math.round](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Math/round) function for numbers; for example threshold(0.49) returns 0, and threshold(0.51) returns 1.

使用默认域 [0.5]和默认范围 [0，1 ] 构造一个新的阈值比例。因此，默认阈值比例等于数字的Math.round函数; 例如阈值（0.49）返回0，阈值（0.51）返回1。

<a name="_threshold" href="#_threshold">#</a> <i>threshold</i>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/threshold.js#L4 "Source")

Given a *value* in the input [domain](#threshold_domain), returns the corresponding value in the output [range](#threshold_range). For example:

给定输入域中的值，返回输出范围中的对应值。例如：

```js
var color = d3.scaleThreshold()
    .domain([0, 1])
    .range(["red", "white", "green"]);

color(-1);   // "red"
color(0);    // "white"
color(0.5);  // "white"
color(1);    // "green"
color(1000); // "green"
```

<a name="threshold_invertExtent" href="#threshold_invertExtent">#</a> <i>threshold</i>.<b>invertExtent</b>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/threshold.js#L21 "Source")

Returns the extent of values in the [domain](#threshold_domain) [<i>x0</i>, <i>x1</i>] for the corresponding *value* in the [range](#threshold_range), representing the inverse mapping from range to domain. This method is useful for interaction, say to determine the value in the domain that corresponds to the pixel location under the mouse. For example:

返回范围中相应值的域 [ x0，x1 ]中值的范围，表示从范围到域的逆映射。这种方法对于交互很有用，比方说确定域中与鼠标下像素位置相对应的值。例如：

```js
var color = d3.scaleThreshold()
    .domain([0, 1])
    .range(["red", "white", "green"]);

color.invertExtent("red"); // [undefined, 0]
color.invertExtent("white"); // [0, 1]
color.invertExtent("green"); // [1, undefined]
```

<a name="threshold_domain" href="#threshold_domain">#</a> <i>threshold</i>.<b>domain</b>([<i>domain</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/threshold.js#L13 "Source")

If *domain* is specified, sets the scale’s domain to the specified array of values. The values must be in sorted ascending order, or the behavior of the scale is undefined. The values are typically numbers, but any naturally ordered values (such as strings) will work; a threshold scale can be used to encode any type that is ordered. If the number of values in the scale’s range is N+1, the number of values in the scale’s domain must be N. If there are fewer than N elements in the domain, the additional values in the range are ignored. If there are more than N elements in the domain, the scale may return undefined for some inputs. If *domain* is not specified, returns the scale’s current domain.

如果指定了域，则将比例域设置为指定的数组值。值必须按升序排序，或者标尺的行为未定义。值通常是数字，但任何自然排序的值（如字符串）都可以使用; 可以使用阈值比例来对任何有序的类型进行编码。如果刻度范围内的值的数量为N + 1，则刻度域中的值的数量必须为N.如果域中少于N个元素，则范围内的其他值将被忽略。如果域中有超过N个元素，则某些输入可能会返回未定义的比例。如果未指定域，则返回比例尺的当前域。

<a name="threshold_range" href="#threshold_range">#</a> <i>threshold</i>.<b>range</b>([<i>range</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/threshold.js#L17 "Source")

If *range* is specified, sets the scale’s range to the specified array of values. If the number of values in the scale’s domain is N, the number of values in the scale’s range must be N+1. If there are fewer than N+1 elements in the range, the scale may return undefined for some inputs. If there are more than N+1 elements in the range, the additional values are ignored. The elements in the given array need not be numbers; any value or type will work. If *range* is not specified, returns the scale’s current range.

如果指定范围，则将比例范围设置为指定的值数组。如果比例域中的值的数量是N，那么比例范围内的值的数量必须是N + 1。如果范围内的元素少于N + 1个，则某些输入可能会返回未定义的比例。如果范围中有超过N + 1个元素，则会忽略其他值。给定数组中的元素不一定是数字; 任何价值或类型将工作。如果未指定范围，则返回比例的当前范围。

<a name="threshold_copy" href="#threshold_copy">#</a> <i>threshold</i>.<b>copy</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/threshold.js#L26 "Source")

Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.

返回此比例的精确副本。此比例的变化不会影响返回的比例，反之亦然。

### Ordinal Scales

Unlike [continuous scales](#continuous-scales), ordinal scales have a discrete domain and range. For example, an ordinal scale might map a set of named categories to a set of colors, or determine the horizontal positions of columns in a column chart.

与连续尺度不同，有序尺度具有离散的域和范围。例如，序号比例可能会将一组命名类别映射到一组颜色，或者确定列图中列的水平位置

<a name="scaleOrdinal" href="#scaleOrdinal">#</a> d3.<b>scaleOrdinal</b>([<i>range</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/ordinal.js "Source")

Constructs a new ordinal scale with an empty [domain](#ordinal_domain) and the specified [*range*](#ordinal_range). If a *range* is not specified, it defaults to the empty array; an ordinal scale always returns undefined until a non-empty range is defined.

用空的域和指定的范围构造一个新的序号比例。如果未指定范围，则默认为空数组; 一个序数标度总是返回undefined，直到定义一个非空范围。

<a name="_ordinal" href="#_ordinal">#</a> <i>ordinal</i>(<i>value</i>) [<>](https://github.com/d3/d3-scale/blob/master/src/ordinal.js#L6 "Source")

Given a *value* in the input [domain](#ordinal_domain), returns the corresponding value in the output [range](#ordinal_range). If the given *value* is not in the scale’s [domain](#ordinal_domain), returns the [unknown](#ordinal_value); or, if the unknown value is [implicit](#scaleImplicit) (the default), then the *value* is implicitly added to the domain and the next-available value in the range is assigned to *value*, such that this and subsequent invocations of the scale given the same input *value* return the same output value.

给定输入域中的值，返回输出范围中的对应值。如果给定的值不在比例域中，则返回未知值 ; 或者，如果未知值是隐式的（缺省值），则该值隐式地添加到域中，并且该范围中的下一个可用值被赋值为值，使得给定相同输入值的该比例和后续调用的调用返回相同的输出值。

<a name="ordinal_domain" href="#ordinal_domain">#</a> <i>ordinal</i>.<b>domain</b>([<i>domain</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/ordinal.js#L22 "Source")

If *domain* is specified, sets the domain to the specified array of values. The first element in *domain* will be mapped to the first element in the range, the second domain value to the second range value, and so on. Domain values are stored internally in a map from stringified value to index; the resulting index is then used to retrieve a value from the range. Thus, an ordinal scale’s values must be coercible to a string, and the stringified version of the domain value uniquely identifies the corresponding range value. If *domain* is not specified, this method returns the current domain.

Setting the domain on an ordinal scale is optional if the [unknown value](#ordinal_unknown) is [implicit](#scaleImplicit) (the default). In this case, the domain will be inferred implicitly from usage by assigning each unique value passed to the scale a new value from the range. Note that an explicit domain is recommended to ensure deterministic behavior, as inferring the domain from usage will be dependent on ordering.

如果域指定，设定域设置为指定值的数组。域中的第一个元素将被映射到范围中的第一个元素，第二个域值到第二个范围值，依此类推。域值内部存储在从字符串化值到索引的映射中; 然后使用生成的索引从范围中检索一个值。因此，序号的值必须可以强制为一个字符串，并且字段值的字符串化版本唯一标识了相应的范围值。如果未指定域，则此方法返回当前域。

如果未知值是隐式的（默认值），则按顺序设置域是可选的。在这种情况下，通过将每个传递给该比例的唯一值分配给该范围中的新值，可以从使用中隐含地推断该域。请注意，建议使用显式域来确保确定性行为，因为从使用中推断域将取决于顺序。

<a name="ordinal_range" href="#ordinal_range">#</a> <i>ordinal</i>.<b>range</b>([<i>range</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/ordinal.js#L30 "Source")

If *range* is specified, sets the range of the ordinal scale to the specified array of values. The first element in the domain will be mapped to the first element in *range*, the second domain value to the second range value, and so on. If there are fewer elements in the range than in the domain, the scale will reuse values from the start of the range. If *range* is not specified, this method returns the current range.

如果范围指定，设定顺序量表设置为指定值的阵列的范围内。域中的第一个元素将被映射到范围中的第一个元素，第二个域值到第二个范围值，依此类推。如果范围内的元素少于域中的元素，则缩放将重新使用范围起始处的值。如果未指定范围，则此方法返回当前范围。

<a name="ordinal_unknown" href="#ordinal_unknown">#</a> <i>ordinal</i>.<b>unknown</b>([<i>value</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/ordinal.js#L34 "Source")

If *value* is specified, sets the output value of the scale for unknown input values and returns this scale. If *value* is not specified, returns the current unknown value, which defaults to [implicit](#implicit). The implicit value enables implicit domain construction; see [*ordinal*.domain](#ordinal_domain).

如果值指定，来设定比例尺为未知的输入值的输出值，并返回这种规模。如果未指定值，则返回当前未知值，该值默认为隐式。隐式值使隐式域构造成为可能; 请参阅序号 .domain。

<a name="ordinal_copy" href="#ordinal_copy">#</a> <i>ordinal</i>.<b>copy</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/ordinal.js#L38 "Source")

Returns an exact copy of this ordinal scale. Changes to this scale will not affect the returned scale, and vice versa.

返回这个序号的精确副本。此比例的变化不会影响返回的比例，反之亦然。

<a name="scaleImplicit" href="#scaleImplicit">#</a> d3.<b>scaleImplicit</b>

A special value for [*ordinal*.unknown](#ordinal_unknown) that enables implicit domain construction: unknown values are implicitly added to the domain.

为有序隐藏域构建的序列 .unknown的特殊值：未知值将隐式添加到域中。

#### Band Scales

Band scales are like [ordinal scales](#ordinal-scales) except the output range is continuous and numeric. Discrete output values are automatically computed by the scale by dividing the continuous range into uniform bands. Band scales are typically used for bar charts with an ordinal or categorical dimension. The [unknown value](#ordinal_unknown) of a band scale is effectively undefined: they do not allow implicit domain construction.

除了输出范围是连续的和数字的以外，带标度就像序数标度。离散输出值通过将连续范围划分为均匀的频带而按比例自动计算。乐谱音阶通常用于具有序号或分类维度的条形图。一个频段的未知值是不确定的：它们不允许隐式域构造。

<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/band.png" width="751" height="238" alt="band">

<a name="scaleBand" href="#scaleBand">#</a> d3.<b>scaleBand</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/band.js "Source")

Constructs a new band scale with the empty [domain](#band_domain), the unit [range](#band_range) [0, 1], no [padding](#band_padding), no [rounding](#band_round) and center [alignment](#band_align).

用空域构造一个新的带标度，单位范围 [0,1]，不填充，不舍入和中心对齐。

<a name="_band" href="#_band">#</a> <i>band</i>(*value*) [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L4 "Source")

Given a *value* in the input [domain](#band_domain), returns the start of the corresponding band derived from the output [range](#band_range). If the given *value* is not in the scale’s domain, returns undefined.

给定输入域中的值，返回从输出范围派生的相应波段的开始。如果给定值不在比例域中，则返回undefined。

<a name="band_domain" href="#band_domain">#</a> <i>band</i>.<b>domain</b>([<i>domain</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L32 "Source")

If *domain* is specified, sets the domain to the specified array of values. The first element in *domain* will be mapped to the first band, the second domain value to the second band, and so on. Domain values are stored internally in a map from stringified value to index; the resulting index is then used to determine the band. Thus, a band scale’s values must be coercible to a string, and the stringified version of the domain value uniquely identifies the corresponding band. If *domain* is not specified, this method returns the current domain.

如果域指定，设定域设置为指定值的数组。域中的第一个元素将映射到第一个band，第二个域的值映射到第二个band，依此类推。域值内部存储在从字符串化值到索引的映射中; 所得到的索引然后用于确定频带。因此，频段的值必须可以强制为一个字符串，并且域值的字符串化版本唯一标识相应的频段。如果未指定域，则此方法返回当前域。

<a name="band_range" href="#band_range">#</a> <i>band</i>.<b>range</b>([<i>range</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L36 "Source")

If *range* is specified, sets the scale’s range to the specified two-element array of numbers. If the elements in the given array are not numbers, they will be coerced to numbers. If *range* is not specified, returns the scale’s current range, which defaults to [0, 1].

如果指定了范围，则将比例范围设置为指定的二元数组数组。如果给定数组中的元素不是数字，它们将被强制为数字。如果未指定范围，则返回比例的当前范围，默认为[0，1]。

<a name="band_rangeRound" href="#band_rangeRound">#</a> <i>band</i>.<b>rangeRound</b>([<i>range</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L40 "Source")

Sets the scale’s [*range*](#band_range) to the specified two-element array of numbers while also enabling [rounding](#band_round). This is a convenience method equivalent to:

将刻度范围设置为指定的两个元素的数字数组，同时启用舍入。这是一种方便的方法，相当于：

```js
band
    .range(range)
    .round(true);
```

Rounding is sometimes useful for avoiding antialiasing artifacts, though also consider the [shape-rendering](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/shape-rendering) “crispEdges” styles.

舍入有时可用于避免抗锯齿工件，但也可以考虑形状渲染 “crispEdges”风格。

<a name="band_round" href="#band_round">#</a> <i>band</i>.<b>round</b>([<i>round</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L52 "Source")

If *round* is specified, enables or disables rounding accordingly. If rounding is enabled, the start and stop of each band will be integers. Rounding is sometimes useful for avoiding antialiasing artifacts, though also consider the [shape-rendering](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/shape-rendering) “crispEdges” styles. Note that if the width of the domain is not a multiple of the cardinality of the range, there may be leftover unused space, even without padding! Use [*band*.align](#band_align) to specify how the leftover space is distributed.

如果指定了round，则启用或禁用相应的舍入。如果启用舍入，每个乐队的开始和停止将是整数。舍入有时可用于避免抗锯齿工件，但也可以考虑形状渲染 “crispEdges”风格。请注意，如果域的宽度不是范围的基数的倍数，那么即使没有填充，也可能存在剩余的未使用空间！使用band .align指定如何分配剩余空间

<a name="band_paddingInner" href="#band_paddingInner">#</a> <i>band</i>.<b>paddingInner</b>([<i>padding</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L60 "Source")

If *padding* is specified, sets the inner padding to the specified value which must be in the range [0, 1]. If *padding* is not specified, returns the current inner padding which defaults to 0. The inner padding determines the ratio of the range that is reserved for blank space between bands.

如果padding被指定，设定所述内padding到指定值，它必须是在范围[0,1]。如果未指定padding，则返回默认为0的当前内部padding。内部padding确定为带之间的空白区域保留的范围的比率。

<a name="band_paddingOuter" href="#band_paddingOuter">#</a> <i>band</i>.<b>paddingOuter</b>([<i>padding</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L64 "Source")

If *padding* is specified, sets the outer padding to the specified value which must be in the range [0, 1]. If *padding* is not specified, returns the current outer padding which defaults to 0. The outer padding determines the ratio of the range that is reserved for blank space before the first band and after the last band.

如果padding被指定，设定外padding到指定值，它必须是在范围[0,1]。如果未指定padding，则返回当前外部padding（默认为0）。外部padding确定在第一个带之前和最后一个带之后为空白区保留的范围的比率。

<a name="band_padding" href="#band_padding">#</a> <i>band</i>.<b>padding</b>([<i>padding</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L56 "Source")

A convenience method for setting the [inner](#band_paddingInner) and [outer](#band_paddingOuter) padding to the same *padding* value. If *padding* is not specified, returns the inner padding.

将内部和外部padding设置为相同padding值的便捷方法。如果未指定padding，则返回内部padding。

<a name="band_align" href="#band_align">#</a> <i>band</i>.<b>align</b>([<i>align</i>]) [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L68 "Source")

If *align* is specified, sets the alignment to the specified value which must be in the range [0, 1]. If *align* is not specified, returns the current alignment which defaults to 0.5. The alignment determines how any leftover unused space in the range is distributed. A value of 0.5 indicates that the leftover space should be equally distributed before the first band and after the last band; *i.e.*, the bands should be centered within the range. A value of 0 or 1 may be used to shift the bands to one side, say to position them adjacent to an axis.

如果align指定，设定align到指定值，必须是在范围[0,1]。如果未指定对齐，则返回当前对齐，默认为0.5。对齐确定了如何分配范围内剩余的未使用空间。值为0.5表示剩余空间在第一个频段之前和最后一个频段之后应该均匀分布; 即频段应该在范围内居中。可以使用值0或1来将波段移到一侧，比如说将它们放置在靠近一个轴的位置。

<a name="band_bandwidth" href="#band_bandwidth">#</a> <i>band</i>.<b>bandwidth</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L44 "Source")

Returns the width of each band.

返回每个band的宽度。

<a name="band_step" href="#band_step">#</a> <i>band</i>.<b>step</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L48 "Source")

Returns the distance between the starts of adjacent bands.

返回相邻波段开始之间的距离。

<a name="band_copy" href="#band_copy">#</a> <i>band</i>.<b>copy</b>() [<>](https://github.com/d3/d3-scale/blob/master/src/band.js#L72 "Source")

Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.

返回此比例的精确副本。此比例的变化不会影响返回的比例，反之亦然。

#### Point Scales

Point scales are a variant of [band scales](#band-scales) with the bandwidth fixed to zero. Point scales are typically used for scatterplots with an ordinal or categorical dimension. The [unknown value](#ordinal_unknown) of a point scale is always undefined: they do not allow implicit domain construction.

点缩放是带宽固定为零的带标尺的变体。点缩放通常用于具有序号或分类维度的散点图。点缩放的未知值始终未定义：它们不允许隐式域构造

<img src="https://raw.githubusercontent.com/d3/d3-scale/master/img/point.png" width="648" height="155" alt="point">

<a name="scalePoint" href="#scalePoint">#</a> d3.<b>scalePoint</b>()

Constructs a new point scale with the empty [domain](#point_domain), the unit [range](#point_range) [0, 1], no [padding](#point_padding), no [rounding](#point_round) and center [alignment](#point_align).

使用空域，单位范围 [0，1]，不填充，不舍入和中心对齐构造一个新的点比例。

<a name="_point" href="#_point">#</a> <i>point</i>(*value*)

Given a *value* in the input [domain](#point_domain), returns the corresponding point derived from the output [range](#point_range). If the given *value* is not in the scale’s domain, returns undefined.

给定输入域中的值，返回从输出范围派生的对应点。如果给定值不在比例域中，则返回undefined。

<a name="point_domain" href="#point_domain">#</a> <i>point</i>.<b>domain</b>([<i>domain</i>])

If *domain* is specified, sets the domain to the specified array of values. The first element in *domain* will be mapped to the first point, the second domain value to the second point, and so on. Domain values are stored internally in a map from stringified value to index; the resulting index is then used to determine the point. Thus, a point scale’s values must be coercible to a string, and the stringified version of the domain value uniquely identifies the corresponding point. If *domain* is not specified, this method returns the current domain.

如果域指定，设定域设置为指定值的数组。域中的第一个元素将被映射到第一个点，第二个域值被映射到第二个点，依此类推。域值内部存储在从字符串化值到索引的映射中; 所得到的索引然后用于确定该点。因此，点标度的值必须可以强制为一个字符串，并且域值的字符串化版本唯一标识相应的点。如果未指定域，则此方法返回当前域。

<a name="point_range" href="#point_range">#</a> <i>point</i>.<b>range</b>([<i>range</i>])

If *range* is specified, sets the scale’s range to the specified two-element array of numbers. If the elements in the given array are not numbers, they will be coerced to numbers. If *range* is not specified, returns the scale’s current range, which defaults to [0, 1].

如果指定了范围，则将比例范围设置为指定的二元数组数组。如果给定数组中的元素不是数字，它们将被强制为数字。如果未指定范围，则返回比例的当前范围，默认为[0，1]。

<a name="point_rangeRound" href="#point_rangeRound">#</a> <i>point</i>.<b>rangeRound</b>([<i>range</i>])

Sets the scale’s [*range*](#point_range) to the specified two-element array of numbers while also enabling [rounding](#point_round). This is a convenience method equivalent to:

将刻度范围设置为指定的两个元素的数字数组，同时启用舍入。这是简写的方法，相当于：

```js
point
    .range(range)
    .round(true);
```

Rounding is sometimes useful for avoiding antialiasing artifacts, though also consider the [shape-rendering](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/shape-rendering) “crispEdges” styles.

舍入有时可用于避免抗锯齿工件，但也可以考虑形状渲染 “crispEdges”风格

<a name="point_round" href="#point_round">#</a> <i>point</i>.<b>round</b>([<i>round</i>])

If *round* is specified, enables or disables rounding accordingly. If rounding is enabled, the position of each point will be integers. Rounding is sometimes useful for avoiding antialiasing artifacts, though also consider the [shape-rendering](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/shape-rendering) “crispEdges” styles. Note that if the width of the domain is not a multiple of the cardinality of the range, there may be leftover unused space, even without padding! Use [*point*.align](#point_align) to specify how the leftover space is distributed.

如果指定了round，则启用或禁用相应的舍入。如果启用舍入，每个点的位置将是整数。舍入有时可用于避免抗锯齿工件，但也可以考虑形状渲染 “crispEdges”风格。请注意，如果域的宽度不是范围的基数的倍数，那么即使没有填充，也可能存在剩余的未使用空间！使用point .align指定剩余空间的分布方式。

<a name="point_padding" href="#point_padding">#</a> <i>point</i>.<b>padding</b>([<i>padding</i>])

If *padding* is specified, sets the outer padding to the specified value which must be in the range [0, 1]. If *padding* is not specified, returns the current outer padding which defaults to 0. The outer padding determines the ratio of the range that is reserved for blank space before the first point and after the last point. Equivalent to [*band*.paddingOuter](#band_paddingOuter).

如果填充被指定，设定外填充到指定值，它必须是在范围[0,1]。如果未指定填充，则返回当前外部填充（默认为0）。外部填充确定第一个点之前和最后一个点之后为空格保留的范围的比例。相当于band .paddingOuter。

<a name="point_align" href="#point_align">#</a> <i>point</i>.<b>align</b>([<i>align</i>])

If *align* is specified, sets the alignment to the specified value which must be in the range [0, 1]. If *align* is not specified, returns the current alignment which defaults to 0.5. The alignment determines how any leftover unused space in the range is distributed. A value of 0.5 indicates that the leftover space should be equally distributed before the first point and after the last point; *i.e.*, the points should be centered within the range. A value of 0 or 1 may be used to shift the points to one side, say to position them adjacent to an axis.

如果对准指定，设定对准到指定值，必须是在范围[0,1]。如果未指定对齐，则返回当前对齐，默认为0.5。对齐确定了如何分配范围内剩余的未使用空间。值为0.5表示剩余空间应该在第一点之前和最后一点之后平均分配; 即点应该在范围内居中。可以使用0或1的值来将点移到一边，比如将它们放置在靠近轴的位置。

<a name="point_bandwidth" href="#point_bandwidth">#</a> <i>point</i>.<b>bandwidth</b>()

Returns zero.

<a name="point_step" href="#point_step">#</a> <i>point</i>.<b>step</b>()

Returns the distance between the starts of adjacent points.

返回相邻点起点之间的距离。

<a name="point_copy" href="#point_copy">#</a> <i>point</i>.<b>copy</b>()

Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.

返回此比例的精确副本。此比例的变化不会影响返回的比例，反之亦然
