# d3-chord

Visualize relationships or network flow with an aesthetically-pleasing circular layout.

弦图用环形布局来清晰地展示关系或者网络流。

[<img alt="Chord Diagram" src="https://raw.githubusercontent.com/d3/d3-chord/master/img/chord.png" width="480" height="480">](http://bl.ocks.org/mbostock/4062006)

## Installing
## 安装

If you use NPM, `npm install d3-chord`. Otherwise, download the [latest release](https://github.com/d3/d3-chord/releases/latest). You can also load directly from [d3js.org](https://d3js.org), either as a [standalone library](https://d3js.org/d3-chord.v1.min.js) or as part of [D3 4.0](https://github.com/d3/d3). AMD, CommonJS, and vanilla environments are supported. In vanilla, a `d3` global is exported:

如果使用NPM,可通过`npm install d3-chord`命令直接安装。
或者通过github下载[最新版本](https://github.com/d3/d3-chord/releases/latest)，也可以通过[d3js.org](https://d3js.org)直接下载[单独的文件](https://d3js.org/d3-chord.v1.min.js)或者整个[D3包](https://github.com/d3/d3)。AMD、 CommonJS和原生环境都支持引用，原生的引入方式如下例：
```html
<script src="https://d3js.org/d3-array.v1.min.js"></script>
<script src="https://d3js.org/d3-path.v1.min.js"></script>
<script src="https://d3js.org/d3-chord.v1.min.js"></script>
<script>

var chord = d3.chord();

</script>
```

[Try d3-chord in your browser.](https://tonicdev.com/npm/d3-chord)

## API Reference
## API 参照

<a href="#chord" name="chord">#</a> d3.<b>chord</b>() [<>](https://github.com/d3/d3-chord/blob/master/src/chord.js "Source")

Constructs a new chord layout with the default settings.

用默认的配置构造一个新的弦布局。

<a href="#_chord" name="_chord">#</a> <i>chord</i>(<i>matrix</i>) [<>](https://github.com/d3/d3-chord/blob/master/src/chord.js#L19 "Source")

Computes the chord layout for the specified square *matrix* of size *n*×*n*, where the *matrix* represents the directed flow amongst a network (a complete digraph) of *n* nodes. The given *matrix* must be an array of length *n*, where each element *matrix*[*i*] is an array of *n* numbers, where each *matrix*[*i*][*j*] represents the flow from the *i*th node in the network to the *j*th node. Each number *matrix*[*i*][*j*] must be nonnegative, though it can be zero if there is no flow from node *i* to node *j*. From the [Circos tableviewer example](http://mkweb.bcgsc.ca/circos/guide/tables/):

给定一个 *n*×*n* 的方形矩阵，函数根据矩阵构造一个弦布局。矩阵表示的是一个网络图（完全有向图）中 *n* 个节点的走向，而且矩阵必须是长度为 *n* 的数组，数组中每个元素 *matrix*[*i*] 也必须是一个数字组成的长度为 *n* 的数组。矩阵中每个值 *matrix*[*i*][*j*] 代表网络图中节点 *i* 到 *j* 的走向，且值必须为非负，0 则表示节点 *i* 到 *j* 之间没有连通。以下是[Circos tableviewer](http://mkweb.bcgsc.ca/circos/guide/tables/)中的例子:

```js
var matrix = [
  [11975,  5871, 8916, 2868],
  [ 1951, 10048, 2060, 6171],
  [ 8010, 16145, 8090, 8045],
  [ 1013,   990,  940, 6907]
];
```

The return value of *chord*(*matrix*) is an array of *chords*, where each chord represents the combined bidirectional flow between two nodes *i* and *j* (where *i* may be equal to *j*) and is an object with the following properties:

* `source` - the source subgroup
* `target` - the target subgroup

函数 *chord*(*matrix*) 的返回值是一个弦对象数组，弦对象表示节点 *i* 和 *j* 之间（*i* 可能等于 *j*）的双向流关系，对象的属性包含：

* `source` - 源子分组
* `target` - 目标子分组


Each source and target subgroup is also an object with the following properties:

* `startAngle` - the start angle in radians
* `endAngle` - the end angle in radians
* `value` - the flow value *matrix*[*i*][*j*]
* `index` - the node index *i*
* `subindex` - the node index *j*

源子分组和目标子分组也分别是包含以下属性的对象:

* `startAngle` - 弧的起始角度，单位为弧度
* `endAngle` - 弧的终止角度，单位为弧度
* `value` - 流数值 *matrix*[*i*][*j*]
* `index` - 节点 *i* 的索引
* `subindex` - 节点 *j* 的索引

The chords are typically passed to [d3.ribbon](#ribbon) to display the network relationships. The returned array includes only chord objects for which the value *matrix*[*i*][*j*] or *matrix*[*j*][*i*] is non-zero. Furthermore, the returned array only contains unique chords: a given chord *ij* represents the bidirectional flow from *i* to *j* *and* from *j* to *i*, and does not contain a duplicate chord *ji*; *i* and *j* are chosen such that the chord’s source always represents the larger of *matrix*[*i*][*j*] and *matrix*[*j*][*i*]. In other words, *chord*.source.index equals *chord*.target.subindex, *chord*.source.subindex equals *chord*.target.index, *chord*.source.value is greater than or equal to *chord*.target.value, and *chord*.source.value is always greater than zero.

弦对象通常作为参数传给[d3.ribbon](#ribbon)方法展示网络关系，方法返回值是只包含非0数值 *matrix*[*i*][*j*] 或 *matrix*[*j*][*i*] 的弦对象数组，且数组中只包含唯一的弦对象：弦对象 *ij* 代表从节点 *i* 到 *j* 和  *j* 到 *i* 的双向流，不存在重复的对象 *ji*。返回弦对象的源子分组表示 *matrix*[*i*][*j*] 和 *matrix*[*j*][*i*] 中的较大值，换句话说： *chord*.source.index 等于 *chord*.target.subindex，*chord*.source.subindex 等于 *chord*.target.index，*chord*.source.value 恒大于0 且 大于等于 *chord*.target.value 。

The *chords* array also defines a secondary array of length *n*, *chords*.groups, where each group represents the combined outflow for node *i*, corresponding to the elements *matrix*[*i*][0 … *n* - 1], and is an object with the following properties:

* `startAngle` - the start angle in radians
* `endAngle` - the end angle in radians
* `value` - the total outgoing flow value for node *i*
* `index` - the node index *i*

*chords* 数组同时也定义了一个二级数组 *chords*.groups，数组长度为n，每个元素表示节点 *i* 的流出对应关系矩阵中的数值 *matrix*[*i*][0 … *n* - 1]，每个元素都是包含以下属性的对象:

* `startAngle` - 弧的起始角度，单位为弧度
* `endAngle` - 弧的终止角度，单位为弧度
* `value` - 节点 *i* 的总共流出值
* `index` - 节点 *i* 的索引

The groups are typically passed to [d3.arc](https://github.com/d3/d3-shape#arc) to produce a donut chart around the circumference of the chord layout.

groups数组通常作为参数传值给方法[d3.arc](https://github.com/d3/d3-shape#arc)，在线布局周围生成一个圈图。 

<a href="#chord_padAngle" name="#chord_padAngle">#</a> <i>chord</i>.<b>padAngle</b>([<i>angle</i>]) [<>](https://github.com/d3/d3-chord/blob/master/src/chord.js#L104 "Source")

If *angle* is specified, sets the pad angle between adjacent groups to the specified number in radians and returns this chord layout. If *angle* is not specified, returns the current pad angle, which defaults to zero.

如果给定了 *angle* 值，就将相邻groups之间的填充设置为对应的弧度后返回对应的弦图；如果未给定 *angle* 值，将返回默认填充值为0的弦图。

<a href="#chord_sortGroups" name="#chord_sortGroups">#</a> <i>chord</i>.<b>sortGroups</b>([<i>compare</i>]) [<>](https://github.com/d3/d3-chord/blob/master/src/chord.js#L108 "Source")

If *compare* is specified, sets the group comparator to the specified function or null and returns this chord layout. If *compare* is not specified, returns the current group comparator, which defaults to null. If the group comparator is non-null, it is used to sort the groups by their total outflow. See also [d3.ascending](https://github.com/d3/d3-array#ascending) and [d3.descending](https://github.com/d3/d3-array#descending).

如果给定了 *compare* 的值，将分组比较器定义为指定的函数或 null 并返回对应的弦图。如果未指定 *compare*，返回的弦图分组比较器为默认值null。分组比较器不为null时，用于根据总的流出量对groups数组排序。同时可参阅[d3.ascending](https://github.com/d3/d3-array#ascending) 和 [d3.descending](https://github.com/d3/d3-array#descending)。

<a href="#chord_sortSubgroups" name="#chord_sortSubgroups">#</a> <i>chord</i>.<b>sortSubgroups</b>([<i>compare</i>]) [<>](https://github.com/d3/d3-chord/blob/master/src/chord.js#L112 "Source")

If *compare* is specified, sets the subgroup comparator to the specified function or null and returns this chord layout. If *compare* is not specified, returns the current subgroup comparator, which defaults to null. If the subgroup comparator is non-null, it is used to sort the subgroups corresponding to *matrix*[*i*][0 … *n* - 1] for a given group *i* by their total outflow. See also [d3.ascending](https://github.com/d3/d3-array#ascending) and [d3.descending](https://github.com/d3/d3-array#descending).

如果给定了 *compare* 的值，将子分组比较器定义为指定的函数或 null 并返回对应的弦图。如果未指定 *compare*，返回的弦图子分组比较器为默认值null。分组比较器不为null时，用于根据总的流出量对子分组数组subgroups排序，传入比较器函数的参数为分组 *i* 对应的 *matrix*[*i*][0 … *n* - 1] 值。同时可参阅[d3.ascending](https://github.com/d3/d3-array#ascending) 和[d3.descending](https://github.com/d3/d3-array#descending)。

<a href="#chord_sortChords" name="#chord_sortChords">#</a> <i>chord</i>.<b>sortChords</b>([<i>compare</i>]) [<>](https://github.com/d3/d3-chord/blob/master/src/chord.js#L116 "Source")

If *compare* is specified, sets the chord comparator to the specified function or null and returns this chord layout. If *compare* is not specified, returns the current chord comparator, which defaults to null. If the chord comparator is non-null, it is used to sort the [chords](#_chord) by their combined flow; this only affects the *z*-order of the chords. See also [d3.ascending](https://github.com/d3/d3-array#ascending) and [d3.descending](https://github.com/d3/d3-array#descending).

如果给定了 *compare* 的值，将弦对象比较器定义为指定的函数或 null 并返回对应的弦图。如果未指定 *compare*，返回的弦图弦对象比较器为默认值null。弦对象比较器不为null时，用于根据弦对象的组合流量对弦对象数组[chords](#_chord)排序，排序结果只影响弦对象数组的z顺序。同时可参阅[d3.ascending](https://github.com/d3/d3-array#ascending) 和[d3.descending](https://github.com/d3/d3-array#descending)。 

<a href="#ribbon" name="ribbon">#</a> d3.<b>ribbon</b>() [<>](https://github.com/d3/d3-chord/blob/master/src/ribbon.js "Source")

Creates a new ribbon generator with the default settings.

用默认配置创建一个带状图生成器。

<a href="#_ribbon" name="_ribbon">#</a> <i>ribbon</i>(<i>arguments…</i>) [<>](https://github.com/d3/d3-chord/blob/master/src/ribbon.js#L34 "Source")

Generates a ribbon for the given *arguments*. The *arguments* are arbitrary; they are simply propagated to the ribbon generator’s accessor functions along with the `this` object. For example, with the default settings, a [chord object](#_chord) expected:

根据给定的参数 *arguments* 生成一个带状图。*arguments* 是自定义的，通过 `this` 对象传给带状图生成器的访问器函数。如下例，默认配置下，传参为弦对象[chord](#_chord):

```js
var ribbon = d3.ribbon();

ribbon({
  source: {startAngle: 0.7524114, endAngle: 1.1212972, radius: 240},
  target: {startAngle: 1.8617078, endAngle: 1.9842927, radius: 240}
}); // "M164.0162810494058,-175.21032946354026A240,240,0,0,1,216.1595644740915,-104.28347273835429Q0,0,229.9158815306728,68.8381247563705A240,240,0,0,1,219.77316791012538,96.43523560788266Q0,0,164.0162810494058,-175.21032946354026Z"
```

Or equivalently if the radius is instead defined as a constant:

也可以传参数为弧度值常量：

```js
var ribbon = d3.ribbon()
    .radius(240);

ribbon({
  source: {startAngle: 0.7524114, endAngle: 1.1212972},
  target: {startAngle: 1.8617078, endAngle: 1.9842927}
}); // "M164.0162810494058,-175.21032946354026A240,240,0,0,1,216.1595644740915,-104.28347273835429Q0,0,229.9158815306728,68.8381247563705A240,240,0,0,1,219.77316791012538,96.43523560788266Q0,0,164.0162810494058,-175.21032946354026Z"
```

If the ribbon generator has a context, then the ribbon is rendered to this context as a sequence of path method calls and this function returns void. Otherwise, a path data string is returned.

如果带状图生成器有上下文环境，带状图将渲染到对应的上下文环境。生成器自动调用一系列的路径生成方法，返回路径字符串数据。

<a href="#ribbon_source" name="ribbon_source">#</a> <i>ribbon</i>.<b>source</b>([<i>source</i>]) [<>](https://github.com/d3/d3-chord/blob/master/src/ribbon.js#L74 "Source")

If *source* is specified, sets the source accessor to the specified function and returns this ribbon generator. If *source* is not specified, returns the current source accessor, which defaults to:

如果给定了 *source* ，则将源访问器函数定义为指定的函数，函数返回带状生成器。如果未指定 *source*，返回当前的默认源访问器函数：

```js
function source(d) {
  return d.source;
}
```

<a href="#ribbon_target" name="ribbon_target">#</a> <i>ribbon</i>.<b>target</b>([<i>target</i>]) [<>](https://github.com/d3/d3-chord/blob/master/src/ribbon.js#L78 "Source")

If *target* is specified, sets the target accessor to the specified function and returns this ribbon generator. If *target* is not specified, returns the current target accessor, which defaults to:

如果给定了 *target* ，则将目标访问器函数定义为指定的函数，函数返回值为带状生成器。如果未指定 *target*，返回当前的默认目标访问器函数：

```js
function target(d) {
  return d.target;
}
```

<a href="#ribbon_radius" name="ribbon_radius">#</a> <i>ribbon</i>.<b>radius</b>([<i>radius</i>]) [<>](https://github.com/d3/d3-chord/blob/master/src/ribbon.js#L62 "Source")

If *radius* is specified, sets the radius accessor to the specified function and returns this ribbon generator. If *radius* is not specified, returns the current radius accessor, which defaults to:

如果给定 *radius*，则将弧度访问器函数定义为指定函数，函数返回值为带状图生成器。如果未指定 *radius*，返回当前的默认弧度访问器函数：

```js
function radius(d) {
  return d.radius;
}
```

<a href="#ribbon_startAngle" name="ribbon_startAngle">#</a> <i>ribbon</i>.<b>startAngle</b>([<i>angle</i>]) [<>](https://github.com/d3/d3-chord/blob/master/src/ribbon.js#L66 "Source")

If *angle* is specified, sets the start angle accessor to the specified function and returns this ribbon generator. If *angle* is not specified, returns the current start angle accessor, which defaults to:

如果给定 *angle*，则将起始角访问器函数定义为指定函数，函数返回值为带状图生成器。如果未指定 *angle*，返回当前的默认起始角访问器函数：

```js
function startAngle(d) {
  return d.startAngle;
}
```

The *angle* is specified in radians, with 0 at -*y* (12 o’clock) and positive angles proceeding clockwise.

*angle* 为从0（12点方向）向顺时针正向增长的弧度值。

<a href="#ribbon_endAngle" name="ribbon_endAngle">#</a> <i>ribbon</i>.<b>endAngle</b>([<i>angle</i>]) [<>](https://github.com/d3/d3-chord/blob/master/src/ribbon.js#L70 "Source")

If *angle* is specified, sets the end angle accessor to the specified function and returns this ribbon generator. If *angle* is not specified, returns the current end angle accessor, which defaults to:

如果给定 *angle*，则将终止角访问器函数定义为指定函数，函数返回值为带状图生成器。如果未指定 *angle*，返回当前的默认终止角访问器函数：

```js
function endAngle(d) {
  return d.endAngle;
}
```

The *angle* is specified in radians, with 0 at -*y* (12 o’clock) and positive angles proceeding clockwise.

*angle* 为从0（12点方向）向顺时针正向增长的弧度值。

<a href="#ribbon_context" name="ribbon_context">#</a> <i>ribbon</i>.<b>context</b>([<i>context</i>]) [<>](https://github.com/d3/d3-chord/blob/master/src/ribbon.js#L82 "Source")

If *context* is specified, sets the context and returns this ribbon generator. If *context* is not specified, returns the current context, which defaults to null. If the context is not null, then the [generated ribbon](#_ribbon) is rendered to this context as a sequence of [path method](http://www.w3.org/TR/2dcontext/#canvaspathmethods) calls. Otherwise, a [path data](http://www.w3.org/TR/SVG/paths.html#PathData) string representing the generated ribbon is returned. See also [d3-path](https://github.com/d3/d3-path).

如果给定了 *context*，定义上下文环境为指定的 *context*并返回对应的带状图生成器。如果未给定 *context* ，则返回默认当前上下文环境null。如果上下文环境不为null，[带状图](#_ribbon)将渲染到对应的上下文环境。生成器自动调用一系列的[路径生成方法](http://www.w3.org/TR/2dcontext/#canvaspathmethods) ，返回表示生成带状图的[路径字符串数据](http://www.w3.org/TR/SVG/paths.html#PathData)。同时可参阅[d3-path](https://github.com/d3/d3-path)。
