[文档源链接](https://github.com/d3/d3-color/blob/master/README.md)

# d3-color

Even though your browser understands a lot about colors, it doesn’t offer much help in manipulating colors through JavaScript. The d3-color module therefore provides representations for various color spaces, allowing specification, conversion and manipulation. (Also see [d3-interpolate](https://github.com/d3/d3-interpolate) for color interpolation.)

即使通过你的浏览器能识别渲染出很多颜色，但是在用js操作colors上也不能提供太多的帮助。因此d3-color模块提供了对色彩空间的各种表示，允许规范、转换和操作。（也可以看[d3-interpolate](https://github.com/d3/d3-interpolate)对color的补充）

For example, take the color named “steelblue”:

例如，可以将颜色命名为“steelblue”（钢蓝色）

```js
var c = d3.color("steelblue"); // {r: 70, g: 130, b: 180, opacity: 1}
```

Let’s try converting it to HSL:

我们试着把它转换成HSL：

```js
var c = d3.hsl("steelblue"); // {h: 207.27…, s: 0.44, l: 0.4902…, opacity: 1}
```

Now rotate the hue by 90°, bump up the saturation, and format as a string for CSS:

现在将色调旋转90度，放大饱和度，并格式化为CSS字符串：

```js
c.h += 90;
c.s += 0.2;
c + ""; // rgb(198, 45, 205)
```

To fade the color slightly:

淡化颜色：

```js
c.opacity = 0.8;
c + ""; // rgba(198, 45, 205, 0.8)
```

In addition to the ubiquitous and machine-friendly [RGB](#rgb) and [HSL](#hsl) color space, d3-color supports two color spaces that are designed for humans:

除了对常见的和人机友好的[RGB](#rgb)和[HSL](#hsl)颜色空间之外，d3-color提供两种给人设计的颜色空间：

* Dave Green’s [Cubehelix](#cubehelix)
* [Lab (CIELAB)](#lab) and [HCL (CIELCH)](#hcl)

* Dave Green 的 [Cubehelix](#cubehelix)
* [Lab (CIELAB)](#lab) 和 [HCL (CIELCH)](#hcl)


Cubehelix features monotonic lightness, while Lab and HCL are perceptually uniform. Note that HCL is the cylindrical form of Lab, similar to how HSL is the cylindrical form of RGB.

cubehelix功能上亮度单调，而L*a*b和HCL在视觉上均匀。注意，HCl是Lab的圆柱形，类似于HSL是RGB的圆柱形。(圆柱形：是一种将RGB色彩模型中的点在圆柱坐标系中的表示法)


## Installing

If you use NPM, `npm install d3-color`. Otherwise, download the [latest release](https://github.com/d3/d3-color/releases/latest). You can also load directly from [d3js.org](https://d3js.org), either as a [standalone library](https://d3js.org/d3-color.v1.min.js) or as part of [D3 4.0](https://github.com/d3/d3). AMD, CommonJS, and vanilla environments are supported. In vanilla, a `d3` global is exported:

如果你用npm，`npm install d3-color`。否则，下载[最新版本](https://github.com/d3/d3-color/releases/latest)。你还可以直接从[d3js.org](https://d3js.org)下载，无论是作为[独立的包](https://d3js.org/d3-color.v1.min.js)还是[D3.4.0](https://github.com/d3/d3)的一部分，AMD，CommonJS和vanilla.js环境中都是支持的。在vanilla中，`d3`是全局出口：

```html
<script src="https://d3js.org/d3-color.v1.min.js"></script>
<script>

var steelblue = d3.rgb("steelblue");

</script>
```

[Try d3-color in your browser.](https://tonicdev.com/npm/d3-color)

## API Reference

<a name="color" href="#color">#</a> d3.<b>color</b>(<i>specifier</i>) [<>](https://github.com/d3/d3-color/blob/master/src/color.js "Source")

Parses the specified [CSS Color Module Level 3](http://www.w3.org/TR/css3-color/#colorunits) *specifier* string, returning an [RGB](#rgb) or [HSL](#hsl) color. If the specifier was not valid, null is returned. Some examples:

解析指定的[css颜色模块级别3](http://www.w3.org/TR/css3-color/#colorunits)字符串，返回一个[RGB](#rgb)或者[HSL](#hsl)颜色，如果说区分符无效，则返回null。举些例子：

* `rgb(255, 255, 255)`
* `rgb(10%, 20%, 30%)`
* `rgba(255, 255, 255, 0.4)`
* `rgba(10%, 20%, 30%, 0.4)`
* `hsl(120, 50%, 20%)`
* `hsla(120, 50%, 20%, 0.4)`
* `#ffeeaa`
* `#fea`
* `steelblue`

The list of supported [named colors](http://www.w3.org/TR/SVG/types.html#ColorKeywords) is specified by CSS.

该列表支持[命名的颜色](http://www.w3.org/TR/SVG/types.html#ColorKeywords)由CSS指定。

Note: this function may also be used with `instanceof` to test if an object is a color instance. The same is true of color subclasses, allowing you to test whether a color is in a particular color space.

注意：如果对象是一个颜色实例，此函数也可用于`instanceof`去测试。颜色子类也是如此，允许你去测试颜色是否在特定颜色空间中。

<a name="color_opacity" href="#color_opacity">#</a> *color*.<b>opacity</b>

This color’s opacity, typically in the range [0, 1].

这种颜色的透明度，通常在范围[0，1]间。

<a name="color_rgb" href="#color_rgb">#</a> *color*.<b>rgb</b>() [<>](https://github.com/d3/d3-color/blob/master/src/color.js#L209 "Source")

Returns the [RGB equivalent](#rgb) of this color. For RGB colors, that’s `this`.

返回这个颜色的[RGB 等值](#rgb)。RGB颜色，就是`this`。

<a name="color_brighter" href="#color_brighter">#</a> *color*.<b>brighter</b>([<i>k</i>]) [<>](https://github.com/d3/d3-color/blob/master/src/color.js#L221 "Source")

Returns a brighter copy of this color. If *k* is specified, it controls how much brighter the returned color should be. If *k* is not specified, it defaults to 1. The behavior of this method is dependent on the implementing color space.

返回这个颜色较亮的副本。如果*k*被指定，则控制返回颜色亮度应该更亮多少。如果*k*没有指定，则它默认为1.这种方法的行为依赖于颜色空间工具。

<a name="color_darker" href="#color_darker">#</a> *color*.<b>darker</b>([<i>k</i>]) [<>](https://github.com/d3/d3-color/blob/master/src/color.js#L225 "Source")

Returns a darker copy of this color. If *k* is specified, it controls how much darker the returned color should be. If *k* is not specified, it defaults to 1. The behavior of this method is dependent on the implementing color space.

返回这个颜色较暗的副本。如果*k*被指定，则控制返回颜色暗度应该更暗多少。如果*k*没有指定，则它默认为1.这种方法的行为依赖于实现颜色空间。

<a name="color_displayable" href="#color_displayable">#</a> *color*.<b>displayable</b>() [<>](https://github.com/d3/d3-color/blob/master/src/color.js#L169 "Source")

Returns true if and only if the color is displayable on standard hardware. For example, this returns false for an RGB color if any channel value is less than zero or greater than 255, or if the opacity is not in the range [0, 1].

如果颜色显示的标准硬件返回的是true，例如，如果有任何的通道值小于0或者大于255，或者不透明不在[0,1]间，则返回RGB颜色为false。

<a name="color_toString" href="#color_toString">#</a> *color*.<b>toString</b>() [<>](https://github.com/d3/d3-color/blob/master/src/color.js#L172 "Source")

Returns a string representing this color according to the [CSS Object Model specification](https://drafts.csswg.org/cssom/#serialize-a-css-component-value), such as `rgb(247, 234, 186)`. If this color is not displayable, a suitable displayable color is returned instead. For example, RGB channel values greater than 255 are clamped to 255.
根据[CSS对象模型](https://drafts.csswg.org/cssom/#serialize-a-css-component-value)返回这个颜色的字符串，如`rgb(247, 234, 186)`。如果这个颜色不能显示，一个合适的颜色返回替代。例如，大于255的RGB通道值会被减小到255。

<a name="rgb" href="#rgb">#</a> d3.<b>rgb</b>(<i>r</i>, <i>g</i>, <i>b</i>[, <i>opacity</i>]) [<>](https://github.com/d3/d3-color/blob/master/src/color.js#L209 "Source")<br>
<a href="#rgb">#</a> d3.<b>rgb</b>(<i>specifier</i>)<br>
<a href="#rgb">#</a> d3.<b>rgb</b>(<i>color</i>)<br>

Constructs a new [RGB](https://en.wikipedia.org/wiki/RGB_color_model) color. The channel values are exposed as `r`, `g` and `b` properties on the returned instance. Use the [RGB color picker](http://bl.ocks.org/mbostock/78d64ca7ef013b4dcf8f) to explore this color space.

构建一种新的[RGB](https://en.wikipedia.org/wiki/RGB_color_model)color。通道值在返回实例中公开`r`, `g` 和 `b`的属性。用[RGB颜色选择器](http://bl.ocks.org/mbostock/78d64ca7ef013b4dcf8f)去查找你的颜色空间。

If *r*, *g* and *b* are specified, these represent the channel values of the returned color; an *opacity* may also be specified. If a CSS Color Module Level 3 *specifier* string is specified, it is parsed and then converted to the RGB color space. See [color](#color) for examples. If a [*color*](#color) instance is specified, it is converted to the RGB color space using [*color*.rgb](#color_rgb). Note that unlike [*color*.rgb](#color_rgb) this method *always* returns a new instance, even if *color* is already an RGB color.

如果*r*，*g*和*b*被指定，则表示返回颜色的通道值；一个*opacity*也可以指定。如果CSS颜色模块级3*specifier*字符串被指定，解析，然后转换到RGB颜色空间。看[color](#color)为例。如果[*color*](#color)实例指定，它被转换到RGB颜色空间使用[*color*.rgb](#color_rgb)。请注意与[*color*.rgb](#color_rgb)这种方法*always*返回一个新的实例，即使*color*已经是RGB颜色

<a name="hsl" href="#hsl">#</a> d3.<b>hsl</b>(<i>h</i>, <i>s</i>, <i>l</i>[, <i>opacity</i>]) [<>](https://github.com/d3/d3-color/blob/master/src/color.js#L281 "Source")<br>
<a href="#hsl">#</a> d3.<b>hsl</b>(<i>specifier</i>)<br>
<a href="#hsl">#</a> d3.<b>hsl</b>(<i>color</i>)<br>

Constructs a new [HSL](https://en.wikipedia.org/wiki/HSL_and_HSV) color. The channel values are exposed as `h`, `s` and `l` properties on the returned instance. Use the [HSL color picker](http://bl.ocks.org/mbostock/debaad4fcce9bcee14cf) to explore this color space.

构建一个新的[HSL](https://en.wikipedia.org/wiki/HSL_and_HSV)color。通道值在返回实例中公开 `h`, `s` 和 `l`的属性。用[HSL颜色选择器](http://bl.ocks.org/mbostock/debaad4fcce9bcee14cf)去查找你的颜色空间。

If *h*, *s* and *l* are specified, these represent the channel values of the returned color; an *opacity* may also be specified. If a CSS Color Module Level 3 *specifier* string is specified, it is parsed and then converted to the HSL color space. See [color](#color) for examples. If a [*color*](#color) instance is specified, it is converted to the RGB color space using [*color*.rgb](#color_rgb) and then converted to HSL. (Colors already in the HSL color space skip the conversion to RGB.)

如果*h*, *s*和*l*被指定，则表示返回颜色的通道值；一个*opacity*也可以指定。如果CSS颜色模块级3*specifier*字符串被指定，解析，然后转换到RGB颜色空间。看[color](#color)为例。如果[*color*](#color)实例指定，它被转换到RGB颜色空间使用[*color*.rgb](#color_rgb)。请注意与[*color*.rgb](#color_rgb)这种方法*always*返回一个新的实例，即使*color*已经是RGB颜色

<a name="lab" href="#lab">#</a> d3.<b>lab</b>(<i>l</i>, <i>a</i>, <i>b</i>[, <i>opacity</i>]) [<>](https://github.com/d3/d3-color/blob/master/src/lab.js#L30 "Source")<br>
<a href="#lab">#</a> d3.<b>lab</b>(<i>specifier</i>)<br>
<a href="#lab">#</a> d3.<b>lab</b>(<i>color</i>)<br>

Constructs a new [Lab](https://en.wikipedia.org/wiki/Lab_color_space#CIELAB) color. The channel values are exposed as `l`, `a` and `b` properties on the returned instance. Use the [Lab color picker](http://bl.ocks.org/mbostock/9f37cc207c0cb166921b) to explore this color space.

构建一种新的[Lab](https://en.wikipedia.org/wiki/Lab_color_space#CIELAB)color。通道值在返回实例中公开`r`, `g` 和 `b`的属性。用[Lab颜色选择器](http://bl.ocks.org/mbostock/9f37cc207c0cb166921b)去查找你的颜色空间。

If *l*, *a* and *b* are specified, these represent the channel values of the returned color; an *opacity* may also be specified. If a CSS Color Module Level 3 *specifier* string is specified, it is parsed and then converted to the Lab color space. See [color](#color) for examples. If a [*color*](#color) instance is specified, it is converted to the RGB color space using [*color*.rgb](#color_rgb) and then converted to Lab. (Colors already in the Lab color space skip the conversion to RGB, and colors in the HCL color space are converted directly to Lab.)

<a name="hcl" href="#hcl">#</a> d3.<b>hcl</b>(<i>h</i>, <i>c</i>, <i>l</i>[, <i>opacity</i>]) [<>](https://github.com/d3/d3-color/blob/master/src/lab.js#L87 "Source")<br>
<a href="#hcl">#</a> d3.<b>hcl</b>(<i>specifier</i>)<br>
<a href="#hcl">#</a> d3.<b>hcl</b>(<i>color</i>)<br>

Constructs a new [HCL](https://en.wikipedia.org/wiki/HCL_color_space) color. The channel values are exposed as `h`, `c` and `l` properties on the returned instance. Use the [HCL color picker](http://bl.ocks.org/mbostock/3e115519a1b495e0bd95) to explore this color space.

构建一种新的[HCL](https://en.wikipedia.org/wiki/HCL_color_space)color。通道值在返回实例中公开`h`, `c` 和 `l`的属性。用[HCL颜色选择器](http://bl.ocks.org/mbostock/3e115519a1b495e0bd95)去查找你的颜色空间。

If *h*, *c* and *l* are specified, these represent the channel values of the returned color; an *opacity* may also be specified. If a CSS Color Module Level 3 *specifier* string is specified, it is parsed and then converted to the HCL color space. See [color](#color) for examples. If a [*color*](#color) instance is specified, it is converted to the RGB color space using [*color*.rgb](#color_rgb) and then converted to HCL. (Colors already in the HCL color space skip the conversion to RGB, and colors in the Lab color space are converted directly to HCL.)

如果*h*, *c*和*l*被指定，则表示返回颜色的通道值；一个*opacity*也可以指定。如果CSS颜色模块级3*specifier*字符串被指定，解析，然后转换到HCL颜色空间。看[color](#color)为例。如果[*color*](#color)实例指定，它被转换到RGB颜色空间使用[*color*.rgb](#color_rgb)然后转换成HCL(Colors已经在HCL颜色空间中跳过转换到RGB,并且colors在Lab颜色空间中直接转换成HCL)

<a name="cubehelix" href="#cubehelix">#</a> d3.<b>cubehelix</b>(<i>h</i>, <i>s</i>, <i>l</i>[, <i>opacity</i>]) [<>](https://github.com/d3/d3-color/blob/master/src/cubehelix.js#L32 "Source")<br>
<a href="#cubehelix">#</a> d3.<b>cubehelix</b>(<i>specifier</i>)<br>
<a href="#cubehelix">#</a> d3.<b>cubehelix</b>(<i>color</i>)<br>

Constructs a new [Cubehelix](https://www.mrao.cam.ac.uk/~dag/CUBEHELIX/) color. The channel values are exposed as `h`, `s` and `l` properties on the returned instance. Use the [Cubehelix color picker](http://bl.ocks.org/mbostock/ba8d75e45794c27168b5) to explore this color space.

构建一种新的[Cubehelix](https://www.mrao.cam.ac.uk/~dag/CUBEHELIX/) color。通道值在返回实例中公开`h`, `s` 和 `l`的属性。用[Cubehelix颜色选择器](http://bl.ocks.org/mbostock/ba8d75e45794c27168b5)去查找你的颜色空间。

If *h*, *s* and *l* are specified, these represent the channel values of the returned color; an *opacity* may also be specified. If a CSS Color Module Level 3 *specifier* string is specified, it is parsed and then converted to the Cubehelix color space. See [color](#color) for examples. If a [*color*](#color) instance is specified, it is converted to the RGB color space using [*color*.rgb](#color_rgb) and then converted to Cubehelix. (Colors already in the Cubehelix color space skip the conversion to RGB.)

如果*h*, *s*和*l*被指定，则表示返回颜色的通道值；一个*opacity*也可以指定。如果CSS颜色模块级3*specifier*字符串被指定，解析，然后转换到Cubehelix颜色空间。看[color](#color)为例。如果[*color*](#color)实例指定，它被转换到RGB颜色空间使用[*color*.rgb](#color_rgb)然后转换成Cubehelix(Colors已经在Cubehelix颜色空间中跳过转换到RGB.)
