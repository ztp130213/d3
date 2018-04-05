[文档源链接](https://github.com/d3/d3-array/blob/master/README.md)

# d3-array

Data in JavaScript is often represented by an array, and so one tends to manipulate arrays when visualizing or analyzing data. Some common forms of manipulation include taking a contiguous slice (subset) of an array, filtering an array using a predicate function, and mapping an array to a parallel set of values using a transform function. Before looking at the set of utilities that this module provides, familiarize yourself with the powerful [array methods built-in to JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/prototype).

在Javascript里数据经常用数组来表示，所以在查看和分析数据是需要操作数组。一些常用的数组操作包括取出一段连续的切片，用一个函数来过滤数组，或者是把用一个转换函数把一个数组映射到另一个数组。在看这个模块提供的数组工具集之前，确保你熟悉强大的[Javascript内建的数组api]((https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/prototype).)

JavaScript includes **mutation methods** that modify the array:

Javascript包含的修改数组方法是 **可变的方法** :

* [*array*.pop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop) - Remove the last element from the array.
* [*array*.push](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push) - Add one or more elements to the end of the array.
* [*array*.reverse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) - Reverse the order of the elements of the array.
* [*array*.shift](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift) - Remove the first element from the array.
* [*array*.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) - Sort the elements of the array.
* [*array*.splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) - Add or remove elements from the array.
* [*array*.unshift](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift) - Add one or more elements to the front of the array.

There are also **access methods** that return some representation of the array:

也包含一些 **接入方法** 用来返回一个数组:

* [*array*.concat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) - Join the array with other array(s) or value(s).
* [*array*.join](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join) - Join all elements of the array into a string.
* [*array*.slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) - Extract a section of the array.
* [*array*.indexOf](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf) - Find the first occurrence of a value within the array.
* [*array*.lastIndexOf](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf) - Find the last occurrence of a value within the array.

And finally **iteration methods** that apply functions to elements in the array:

当然也包括一些 **迭代方法** 用来把一个函数应用于数组的元素上:

* [*array*.filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) - Create a new array with only the elements for which a predicate is true.
* [*array*.forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) - Call a function for each element in the array.
* [*array*.every](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every) - See if every element in the array satisfies a predicate.
* [*array*.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) - Create a new array with the result of calling a function on every element in the array.
* [*array*.some](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some) - See if at least one element in the array satisfies a predicate.
* [*array*.reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) - Apply a function to reduce the array to a single value (from left-to-right).
* [*array*.reduceRight](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight) - Apply a function to reduce the array to a single value (from right-to-left).

## Installing
## 安装

If you use NPM, `npm install d3-array`. Otherwise, download the [latest release](https://github.com/d3/d3-array/releases/latest). You can also load directly from [d3js.org](https://d3js.org), either as a [standalone library](https://d3js.org/d3-array.v1.min.js) or as part of [D3 4.0](https://github.com/d3/d3). AMD, CommonJS, and vanilla environments are supported. In vanilla, a `d3` global is exported:

```html
<script src="https://d3js.org/d3-array.v1.min.js"></script>
<script>

var min = d3.min(array);

</script>
```

[Try d3-array in your browser.](https://tonicdev.com/npm/d3-array)

## API Reference

* [Statistics](#statistics)
* [Search](#search)
* [Transformations](#transformations)
* [Histograms](#histograms)
* [Histogram Thresholds](#histogram-thresholds)

### Statistics

### 统计

Methods for computing basic summary statistics.

基本汇总统计方法。

<a name="min" href="#min">#</a> d3.<b>min</b>(<i>array</i>[, <i>accessor</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/min.js "Source")

Returns the minimum value in the given *array* using natural order. If the array is empty, returns undefined. An optional *accessor* function may be specified, which is equivalent to calling *array*.map(*accessor*) before computing the minimum value.

返回给定数组中自然排序最小的值。如果数组为空，返回undefined。如果指定了*accessor*参数，则在计算最小值之前调用*array*.map(*accessor*)方法。

Unlike the built-in [Math.min](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Math/min), this method ignores undefined, null and NaN values; this is useful for ignoring missing data. In addition, elements are compared using natural order rather than numeric order. For example, the minimum of the strings [“20”, “3”] is “20”, while the minimum of the numbers [20, 3] is 3.

不同于内置的[Math.min](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Math/min)，这个方法会忽略undefined，null和NaN；这对处理数据不全的数组很友好。另外，元素的比较用的是自然排序而不是数字排序。例如，["20","3"]的最小值是20，而[20,3]的最小值是3。

See also [scan](#scan) and [extent](#extent).

<a name="max" href="#max">#</a> d3.<b>max</b>(<i>array</i>[, <i>accessor</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/max.js "Source")

Returns the maximum value in the given *array* using natural order. If the array is empty, returns undefined. An optional *accessor* function may be specified, which is equivalent to calling *array*.map(*accessor*) before computing the maximum value.

返回给定数组中自然排序最大的值。如果数组为空，返回undefined。如果指定了*accessor*参数，则在计算最大值之前调用了*array*.map(*accessor*)方法。

Unlike the built-in [Math.max](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Math/max), this method ignores undefined values; this is useful for ignoring missing data. In addition, elements are compared using natural order rather than numeric order. For example, the maximum of the strings [“20”, “3”] is “3”, while the maximum of the numbers [20, 3] is 20.

不同于内置的[Math.max](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Math/max)，这个方法会忽略未定义的值；这对忽略数组中丢失的数据很有用处。另外，元素的比较用的是自然排序而不是数字排序。例如，["20","3"]的最大值是3，然而[20,3]的最大值是20。

See also [scan](#scan) and [extent](#extent).

<a name="extent" href="#extent">#</a> d3.<b>extent</b>(<i>array</i>[, <i>accessor</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/extent.js "Source")

Returns the [minimum](#min) and [maximum](#max) value in the given *array* using natural order. If the array is empty, returns [undefined, undefined]. An optional *accessor* function may be specified, which is equivalent to calling *array*.map(*accessor*) before computing the extent.

返回给定数组中自然排序的[最小值](#min)和[最大值](#max)。如果数组为空，返回[undefined, undefined]。如果指定了*accessor*参数，则在在计算之前调用了*array*.map(*accessor*)方法。

<a name="sum" href="#sum">#</a> d3.<b>sum</b>(<i>array</i>[, <i>accessor</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/sum.js "Source")

Returns the sum of the given *array* of numbers. If the array is empty, returns 0. An optional *accessor* function may be specified, which is equivalent to calling *array*.map(*accessor*) before computing the sum. This method ignores undefined and NaN values; this is useful for ignoring missing data.

返回给定数组（array）的和。如果数组为空，返回0。如果指定可选参数*accessor*函数，则在计算和之前调用array.map(accessor)。此方法忽略NaN和undefined；这对处理定含未定义值的数组时很有用处。

<a name="mean" href="#mean">#</a> d3.<b>mean</b>(<i>array</i>[, <i>accessor</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/mean.js "Source")

Returns the mean of the given *array* of numbers. If the array is empty, returns undefined. An optional *accessor* function may be specified, which is equivalent to calling *array*.map(*accessor*) before computing the mean. This method ignores undefined and NaN values; this is useful for ignoring missing data.

返回给定数组的平均数。如果数组为空，返回undefined。如果指定可选参数*accessor*函数，则在计算平均数之前调用*array*.map(*accessor*)。此方法忽略非数值(NaN)和undefined；这对处理定含未定义值的数组时很有用处。

<a name="median" href="#median">#</a> d3.<b>median</b>(<i>array</i>[, <i>accessor</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/median.js "Source")

Returns the median of the given *array* of numbers using the [R-7 method](https://en.wikipedia.org/wiki/Quantile#Estimating_quantiles_from_a_sample). If the array is empty, returns undefined. An optional *accessor* function may be specified, which is equivalent to calling *array*.map(*accessor*) before computing the median. This method ignores undefined and NaN values; this is useful for ignoring missing data.

返回给定数组以[R-7算法](https://en.wikipedia.org/wiki/Quantile#Estimating_quantiles_from_a_sample)算出的中位数。如果数组为空，返回undefined。如果指定可选参数accessor，则在计算中位数之前调用*array*.map(*accessor*)。此方法忽略无效值(如NaN和undefined)；这对处理定含未定义值的数组时很有用处。

<a name="quantile" href="#quantile">#</a> d3.<b>quantile</b>(<i>array</i>, <i>p</i>[, <i>accessor</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/quantile.js "Source")

Returns the *p*-quantile of the given **sorted** *array* of numbers, where *p* is a number in the range [0, 1]. For example, the median can be computed using *p* = 0.5, the first quartile at *p* = 0.25, and the third quartile at *p* = 0.75. This particular implementation uses the [R-7 method](http://en.wikipedia.org/wiki/Quantile#Quantiles_of_a_population), which is the default for the R programming language and Excel. For example:

返回给定有序数值数组的p分位数，其中*p*是一个0到1范围的数。例如，中位数可以由*p* = 0.5计算，第一个四分位数是*p* = 0.25，第三个四分位数是*p* = 0.75。这个方法特意用[R-7算法](http://en.wikipedia.org/wiki/Quantile#Quantiles_of_a_population)实现，R编程语言和Excel默认的方式。

```js
var a = [0, 10, 30];
d3.quantile(a, 0); // 0
d3.quantile(a, 0.5); // 10
d3.quantile(a, 1); // 30
d3.quantile(a, 0.25); // 5
d3.quantile(a, 0.75); // 20
d3.quantile(a, 0.1); // 2
```

An optional *accessor* function may be specified, which is equivalent to calling *array*.map(*accessor*) before computing the quantile.

如果指定可选参数*accessor*，相当于在计算中位数之前调用array.map(accessor)。

<a name="variance" href="#variance">#</a> d3.<b>variance</b>(<i>array</i>[, <i>accessor</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/variance.js "Source")

Returns an [unbiased estimator of the population variance](http://mathworld.wolfram.com/SampleVariance.html) of the given *array* of numbers. If the array has fewer than two values, returns undefined. An optional *accessor* function may be specified, which is equivalent to calling *array*.map(*accessor*) before computing the variance. This method ignores undefined and NaN values; this is useful for ignoring missing data.

返回给定数值数组的[无偏总体方差](http://mathworld.wolfram.com/SampleVariance.html)。如果数组的长度小于2，返回undefined。如果知道可选参数*accessor*，则在计算方差之前调用*array*.map(*accessor*)。此方法忽略无效值(如NaN和undefined)；这对处理定含未定义值的数组时很有用处。

<a name="deviation" href="#deviation">#</a> d3.<b>deviation</b>(<i>array</i>[, <i>accessor</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/deviation.js "Source")

Returns the standard deviation, defined as the square root of the [bias-corrected variance](#variance), of the given *array* of numbers. If the array has fewer than two values, returns undefined. An optional *accessor* function may be specified, which is equivalent to calling *array*.map(*accessor*) before computing the standard deviation. This method ignores undefined and NaN values; this is useful for ignoring missing data.

返回给定数值数组的标准差，即方差[bias-corrected variance](#variance)的平方根。如果数组的长度小于2，返回undefined。可选参数accessor被指定，等同在计算中位数之前调用array.map(accessor)。此方法忽略无效值(如NaN和undefined)；这对处理定含未定义值的数组时很有用处。


### Search

### 搜索

Methods for searching arrays for a specific element.

搜索数组特定元素方法。

<a name="scan" href="#scan">#</a> d3.<b>scan</b>(<i>array</i>[, <i>comparator</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/scan.js "Source")

Performs a linear scan of the specified *array*, returning the index of the least element according to the specified *comparator*. If the given *array* contains no comparable elements (*i.e.*, the comparator returns NaN when comparing each element to itself), returns undefined. If *comparator* is not specified, it defaults to [ascending](#ascending). For example:

根据比较函数comparator线性扫描一个数组，返回最后一个元素的索引。如果给定的数组不包含可比较的元素（比如说comparator比较元素自己时返回NaN），返回undefined。如果comparator没有指定，默认[升序排序](#ascending)。例如：

```js
var array = [{foo: 42}, {foo: 91}];
d3.scan(array, function(a, b) { return a.foo - b.foo; }); // 0
d3.scan(array, function(a, b) { return b.foo - a.foo; }); // 1
```

This function is similar to [min](#min), except it allows the use of a comparator rather than an accessor and it returns the index instead of the accessed value. See also [bisect](#bisect).

这个函数有点像[最小值](#min)，除了它允许我们使用*comparator*而不是*accessor*，并且它返回的是索引而不是值。也可以参见[bisect](#bisect).

<a name="bisectLeft" href="#bisectLeft">#</a> d3.<b>bisectLeft</b>(<i>array</i>, <i>x</i>[, <i>lo</i>[, <i>hi</i>]]) [<>](https://github.com/d3/d3-array/blob/master/src/bisect.js#L6 "Source")

Returns the insertion point for *x* in *array* to maintain sorted order. The arguments *lo* and *hi* may be used to specify a subset of the array which should be considered; by default the entire array is used. If *x* is already present in *array*, the insertion point will be before (to the left of) any existing entries. The return value is suitable for use as the first argument to [splice](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/splice) assuming that *array* is already sorted. The returned insertion point *i* partitions the *array* into two halves so that all *v* < *x* for *v* in *array*.slice(*lo*, *i*) for the left side and all *v* >= *x* for *v* in *array*.slice(*i*, *hi*) for the right side.

返回x在给定数组中的插入点，以保持原有顺序。参数lo和hi用来指定数组的子集；默认情况下整个数组都。如果*x*在*array*中已存在，插入点在所有元素之前（左侧）。返回值可用于[splice](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/splice)有序数组的第一个参数。返回的插入点*i*把数组分为两个区：数组中所有array.slice(lo, i)中v<x的v在左边，数组中所有array.slice(i, hi)中v >= x的v在右边。

<a name="bisect" href="#bisect">#</a> d3.<b>bisect</b>(<i>array</i>, <i>x</i>[, <i>lo</i>[, <i>hi</i>]]) [<>](https://github.com/d3/d3-array/blob/master/src/bisect.js "Source")<br>
<a name="bisectRight" href="#bisectRight">#</a> d3.<b>bisectRight</b>(<i>array</i>, <i>x</i>[, <i>lo</i>[, <i>hi</i>]]) [<>](https://github.com/d3/d3-array/blob/master/src/bisect.js#L6 "Source")

Similar to [bisectLeft](#bisectLeft), but returns an insertion point which comes after (to the right of) any existing entries of *x* in *array*. The returned insertion point *i* partitions the *array* into two halves so that all *v* <= *x* for *v* in *array*.slice(*lo*, *i*) for the left side and all *v* > *x* for *v* in *array*.slice(*i*, *hi*) for the right side.

和[bisectLeft](#bisectLeft)类似，但返回插入点来自于数组array中任意实体x之后（右侧）。返回的插入点i把数组分为两个区：数组中所有array.slice(lo, i)中v <= x的v在左边，数组中所有 array.slice(i, hi)中v > x 的v在右边。

<a name="bisector" href="#bisector">#</a> d3.<b>bisector</b>(<i>accessor</i>) [<>](https://github.com/d3/d3-array/blob/master/src/bisector.js "Source")
<br><a name="bisector" href="#bisector">#</a> d3.<b>bisector</b>(<i>comparator</i>) [<>](https://github.com/d3/d3-array/blob/master/src/bisector.js "Source")

Returns a new bisector using the specified *accessor* or *comparator* function. This method can be used to bisect arrays of objects instead of being limited to simple arrays of primitives. For example, given the following array of objects:

使用指定参数*accessor*或者*comparator*函数返回一个二等分线。这个方法能用于二等分对象数组而不适用于原始的简单数组。例如下列对象的数组:

```js
var data = [
  {date: new Date(2011, 1, 1), value: 0.5},
  {date: new Date(2011, 2, 1), value: 0.6},
  {date: new Date(2011, 3, 1), value: 0.7},
  {date: new Date(2011, 4, 1), value: 0.8}
];
```

A suitable bisect function could be constructed as:

一个合适的二等分函数可定义为：

```js
var bisectDate = d3.bisector(function(d) { return d.date; }).right;
```

This is equivalent to specifying a comparator:

相当于指定一个比较器

```js
var bisectDate = d3.bisector(function(d, x) { return d.date - x; }).right;
```

And then applied as *bisectDate*(*array*, *date*), returning an index. Note that the comparator is always passed the search value *x* as the second argument. Use a comparator rather than an accessor if you want values to be sorted in an order different than natural order, such as in descending rather than ascending order.

然后调用*bisectDate*(*array*, *date*)，返回索引。 如果你想使用不同于自然排序的方法对值进行排序，那么可以使用比较器（comparator）而不是访问器（accessor），例如使用降序排序而不是升序排序的时候。

<a name="bisector_left" href="#bisector_left">#</a> <i>bisector</i>.<b>left</b>(<i>array</i>, <i>x</i>[, <i>lo</i>[, <i>hi</i>]]) [<>](https://github.com/d3/d3-array/blob/master/src/bisector.js#L6 "Source")

Equivalent to [bisectLeft](#bisectLeft), but uses this bisector’s associated comparator.

相当于[bisectLeft](#bisectLeft)，只是使用bisector设置的比较器。

<a name="bisector_right" href="#bisector_right">#</a> <i>bisector</i>.<b>right</b>(<i>array</i>, <i>x</i>[, <i>lo</i>[, <i>hi</i>]]) [<>](https://github.com/d3/d3-array/blob/master/src/bisector.js#L16 "Source")

Equivalent to [bisectRight](#bisectRight), but uses this bisector’s associated comparator.

相当于[bisectRight](#bisectRight)，只是使用bisector设置的比较器。

<a name="ascending" href="#ascending">#</a> d3.<b>ascending</b>(<i>a</i>, <i>b</i>) [<>](https://github.com/d3/d3-array/blob/master/src/ascending.js "Source")

Returns -1 if *a* is less than *b*, or 1 if *a* is greater than *b*, or 0. This is the comparator function for natural order, and can be used in conjunction with the built-in [*array*.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) method to arrange elements in ascending order. It is implemented as:

如果a<b返回-1，a>b返回1，a=b返回0。默认的比较器是自然排序，也可用于关联内置[*array*.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)方法来给元素升序排序。实现如下：

```js
function ascending(a, b) {
  return a < b ? -1 : a > b ? 1 : a >= b ? 0 : NaN;
}
```

Note that if no comparator function is specified to the built-in sort method, the default order is lexicographic (alphabetical), not natural! This can lead to surprising behavior when sorting an array of numbers.

注意，如果没有给数组的内置排序方法没有指定比较器函数，那默认的排序是字典排序(字母序)，而非自然排列！所以给数值数组排序时会有bug。

<a name="descending" href="#descending">#</a> d3.<b>descending</b>(<i>a</i>, <i>b</i>) [<>](https://github.com/d3/d3-array/blob/master/src/descending.js "Source")

Returns -1 if *a* is greater than *b*, or 1 if *a* is less than *b*, or 0. This is the comparator function for reverse natural order, and can be used in conjunction with the built-in array sort method to arrange elements in descending order.  It is implemented as:

如果a>b返回-1，a<b返回1，a=b返回0。默认的比较器是自然排序，也可关联内置[*array*.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)方法来给元素降序序排序。实现如下：

```js
function descending(a, b) {
  return b < a ? -1 : b > a ? 1 : b >= a ? 0 : NaN;
}
```

Note that if no comparator function is specified to the built-in sort method, the default order is lexicographic (alphabetical), not natural! This can lead to surprising behavior when sorting an array of numbers.

注意，如果没有给数组的内置排序方法没有指定比较器函数，那默认的排序是字典排序(字母序)，而非自然排列！所以给数值数组排序时会有bug。

### Transformations

### 变换

Methods for transforming arrays and for generating new arrays.

变换一个数组并生成新数组的方法。

<a name="cross" href="#cross">#</a> d3.<b>cross</b>(<i>a</i>, <i>b</i>[, <i>reducer</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/cross.js "Source")

Returns the [Cartesian product](https://en.wikipedia.org/wiki/Cartesian_product) of the two arrays *a* and *b*. For each element *i* in the specified array *a* and each element *j* in the specified array *b*, in order, invokes the specified *reducer* function passing the element *i* and element *j*. If a *reducer* is not specified, it defaults to a function which creates a two-element array for each pair:

返回数组*a*和*b*的笛卡尔积。把数组*a*中的每个元素*i*和数组*b*中的每个元素*j*, 按顺序传入指定的*reudece*方法。如果没有指定*reducer*方法，默认会生成一个两个元素的数组。

```js
function pair(a, b) {
  return [a, b];
}
```

For example:

例如：

```js
d3.cross([1, 2], ["x", "y"]); // returns [[1, "x"], [1, "y"], [2, "x"], [2, "y"]]
d3.cross([1, 2], ["x", "y"], (a, b) => a + b); // returns ["1x", "1y", "2x", "2y"]
```

<a name="merge" href="#merge">#</a> d3.<b>merge</b>(<i>arrays</i>) [<>](https://github.com/d3/d3-array/blob/master/src/merge.js "Source")

Merges the specified *arrays* into a single array. This method is similar to the built-in array concat method; the only difference is that it is more convenient when you have an array of arrays.

合并指定多个数组为一个数组，此方法和数组内置方法concat类似；唯一不同是当你要处理多维数组时，d3.merge(arrays)方法更方便。

```js
d3.merge([[1], [2, 3]]); // returns [1, 2, 3]
```

<a name="pairs" href="#pairs">#</a> d3.<b>pairs</b>(<i>array</i>[, <i>reducer</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/pairs.js "Source")

For each adjacent pair of elements in the specified *array*, in order, invokes the specified *reducer* function passing the element *i* and element *i* - 1. If a *reducer* is not specified, it defaults to a function which creates a two-element array for each pair:

对指定*array*中每个相邻元素对，将元素*i*和元素*i*-1按顺序传给指定的*reducer*。如果*ruducer*没有指定，默认创建一个两个元素的数组对：

```js
function pair(a, b) {
  return [a, b];
}
```

For example:

```js
d3.pairs([1, 2, 3, 4]); // returns [[1, 2], [2, 3], [3, 4]]
d3.pairs([1, 2, 3, 4], (a, b) => b - a); // returns [1, 1, 1];
```

If the specified array has fewer than two elements, returns the empty array.

如果指定参数array中少于两个元素，则返回一个空数组。

<a name="permute" href="#permute">#</a> d3.<b>permute</b>(<i>array</i>, <i>indexes</i>) [<>](https://github.com/d3/d3-array/blob/master/src/permute.js "Source")

Returns a permutation of the specified *array* using the specified array of *indexes*. The returned array contains the corresponding element in array for each index in indexes, in order. For example, permute(["a", "b", "c"], [1, 2, 0])
returns ["b", "c", "a"]. It is acceptable for the array of indexes to be a different length from the array of elements, and for indexes to be duplicated or omitted.

使用指定的*indexes*数组返回数组的转置。返回数组包含indexes数组中索引按顺序对应的元素。例如，permute(["a", "b", "c"], [1, 2, 0]) 返回 ["b", "c", "a"]。indexes长度和array长度不一样是可以接受的，indexes中的元素将会重复或者省略。

This method can also be used to extract the values from an object into an array with a stable order. Extracting keyed values in order can be useful for generating data arrays in nested selections. For example:

这个方法可以用来按固定顺序提取对象中的值到一个数组中。按顺序提取带键的值可以用来生成嵌套选择中的数据数组。例如：

```js
var object = {yield: 27, variety: "Manchuria", year: 1931, site: "University Farm"},
    fields = ["site", "variety", "yield"];

d3.permute(object, fields); // returns ["University Farm", "Manchuria", 27]
```

<a name="shuffle" href="#shuffle">#</a> d3.<b>shuffle</b>(<i>array</i>[, <i>lo</i>[, <i>hi</i>]]) [<>](https://github.com/d3/d3-array/blob/master/src/shuffle.js "Source")

Randomizes the order of the specified *array* using the [Fisher–Yates shuffle](http://bost.ocks.org/mike/shuffle/).

使用[费雪耶兹随机置乱算法](http://bost.ocks.org/mike/shuffle/)随机打乱给定数组的顺序。

<a name="ticks" href="#ticks">#</a> d3.<b>ticks</b>(<i>start</i>, <i>stop</i>, <i>count</i>) [<>](https://github.com/d3/d3-array/blob/master/src/ticks.js "Source")

Returns an array of approximately *count* + 1 uniformly-spaced, nicely-rounded values between *start* and *stop* (inclusive). Each value is a power of ten multiplied by 1, 2 or 5. See also [d3.tickIncrement](#tickIncrement), [d3.tickStep](#tickStep) and [*linear*.ticks](https://github.com/d3/d3-scale/blob/master/README.md#linear_ticks).

返回一个介于*start*和*stop*(包括)之间*count* + 1近似等分数组。每个值都是10的指数（1,2或5）次方。也可以参考[[d3.tickIncrement](#tickIncrement)，[d3.tickStep](#tickStep)和[*linear*.ticks](https://github.com/d3/d3-scale/blob/master/README.md#linear_ticks)。

Ticks are inclusive in the sense that they may include the specified *start* and *stop* values if (and only if) they are exact, nicely-rounded values consistent with the inferred [step](#tickStep). More formally, each returned tick *t* satisfies *start* ≤ *t* and *t* ≤ *stop*.

当且仅当*start*到*stop*能正好分到step份时才包含start和stop。更多情况，每个步长*t*满足*start*≤ *t* 并且 *t* ≤ *stop*。

<a name="tickIncrement" href="#tickIncrement">#</a> d3.<b>tickIncrement</b>(<i>start</i>, <i>stop</i>, <i>count</i>) [<>](https://github.com/d3/d3-array/blob/master/src/ticks.js#L16 "Source")

Like [d3.tickStep](#tickStep), except requires that *start* is always less than or equal to *step*, and if the tick step for the given *start*, *stop* and *count* would be less than one, returns the negative inverse tick step instead. This method is always guaranteed to return an integer, and is used by [d3.ticks](#ticks) to avoid guarantee that the returned tick values are represented as precisely as possible in IEEE 754 floating point.

像[d3.tickStep](#tickStep)，除了需要*start*小于等于*stop*外，如果给的*count*小于1，返回的分割将会用负的步长。这个方法总是会返回一个整数，[d3.ticks](#ticks)调用时返回的数值尽量满足IEEE 754的精度。

<a name="tickStep" href="#tickStep">#</a> d3.<b>tickStep</b>(<i>start</i>, <i>stop</i>, <i>count</i>) [<>](https://github.com/d3/d3-array/blob/master/src/ticks.js#L16 "Source")

Returns the difference between adjacent tick values if the same arguments were passed to [d3.ticks](#ticks): a nicely-rounded value that is a power of ten multiplied by 1, 2 or 5. Note that due to the limited precision of IEEE 754 floating point, the returned value may not be exact decimals; use [d3-format](https://github.com/d3/d3-format) to format numbers for human consumption.

把相同的参数传给[d3.ticks](#ticks)相比，相邻tick不同的地方是：近似的值是10的1,2或5次方。注意精度受IEEE 754的限制，返回的数值可能不是精确的小数；用 [d3-format](https://github.com/d3/d3-format)格式化数字变成可读的数字。

<a name="range" href="#range">#</a> d3.<b>range</b>([<i>start</i>, ]<i>stop</i>[, <i>step</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/range.js "Source")

Returns an array containing an arithmetic progression, similar to the Python built-in [range](http://docs.python.org/library/functions.html#range). This method is often used to iterate over a sequence of uniformly-spaced numeric values, such as the indexes of an array or the ticks of a linear scale. (See also [d3.ticks](#ticks) for nicely-rounded values.)

生成一个包含算数级数的数组，类似于Python的内置函数[range](http://docs.python.org/library/functions.html#range)。这个方法常用来遍历一个数字序列或者整型数值。例如数组中的索引或者线性比例尺的刻度。

If *step* is omitted, it defaults to 1. If *start* is omitted, it defaults to 0. The *stop* value is exclusive; it is not included in the result. If *step* is positive, the last element is the largest *start* + *i* \* *step* less than *stop*; if *step* is negative, the last element is the smallest *start* + *i* \* *step* greater than *stop*. If the returned array would contain an infinite number of values, an empty range is returned.

如果省略step，默认值是1。如果省略*start*参数，默认值就是0。结果中不包含*stop*值。如果*step*是正的，则最后一个元素是小于*stop*的最大*start* + *i* \* *step*; 如果*step*是负的，最后一个元素是大于*stop*的最小*start* + *i* \* *step*。如果结果数组中包含无限循环小数，将会返回一个空的范围。

The arguments are not required to be integers; however, the results are more predictable if they are. The values in the returned array are defined as *start* + *i* \* *step*, where *i* is an integer from zero to one minus the total number of elements in the returned array. For example:

参数不要求是整型；但是，如果它们是整型数结果会可预见些。返回数组的元素是*start* + *i* \* *step*，*i*是0到返回数组长度-1的整数。例如：

```js
d3.range(0, 1, 0.2) // [0, 0.2, 0.4, 0.6000000000000001, 0.8]
```

This unexpected behavior is due to IEEE 754 double-precision floating point, which defines 0.2 * 3 = 0.6000000000000001. Use [d3-format](https://github.com/d3/d3-format) to format numbers for human consumption with appropriate rounding; see also [linear.tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#linear_tickFormat) in [d3-scale](https://github.com/d3/d3-scale).

上面这个不符合预期的行为是IEEE 754双精度浮点数引起的，0.2 * 3 = 0.6000000000000001。使用[d3-format](https://github.com/d3/d3-format)近似格式化数据；也可以查看d3-scale](https://github.com/d3/d3-scale)的[linear.tickFormat](https://github.com/d3/d3-scale/blob/master/README.md#linear_tickFormat)。

Likewise, if the returned array should have a specific length, consider using [array.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) on an integer range. For example:

同样的，如果返回的数组的长度固定，可以在一个整数的range上使用[array.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)。例如：

```js
d3.range(0, 1, 1 / 49); // BAD: returns 50 elements!
d3.range(49).map(function(d) { return d / 49; }); // GOOD: returns 49 elements.
```

<a name="transpose" href="#transpose">#</a> d3.<b>transpose</b>(<i>matrix</i>) [<>](https://github.com/d3/d3-array/blob/master/src/transpose.js "Source")

Uses the [zip](#zip) operator as a two-dimensional [matrix transpose](http://en.wikipedia.org/wiki/Transpose).

使用zip操作符作为二维[矩阵变换](http://en.wikipedia.org/wiki/Transpose)。

<a name="zip" href="#zip">#</a> d3.<b>zip</b>(<i>arrays…</i>) [<>](https://github.com/d3/d3-array/blob/master/src/zip.js "Source")

Returns an array of arrays, where the *i*th array contains the *i*th element from each of the argument *arrays*. The returned array is truncated in length to the shortest array in *arrays*. If *arrays* contains only a single array, the returned array contains one-element arrays. With no arguments, the returned array is empty.

返回的数组的数组，其中，第i个数组包含来自每个arrays参数的第i个元素。返回的数组长度被截断为arrays中最短数组的长度。如果arrays只包含一个数组，则返回的数组是只包含一个元素的数组。如果不带任何参数，则返回的数组是空的。

```js
d3.zip([1, 2], [3, 4]); // returns [[1, 3], [2, 4]]
```

### Histograms

### 直方图

[<img src="https://raw.githubusercontent.com/d3/d3-array/master/img/histogram.png" width="480" height="250" alt="Histogram">](http://bl.ocks.org/mbostock/3048450)

Histograms bin many discrete samples into a smaller number of consecutive, non-overlapping intervals. They are often used to visualize the distribution of numerical data.

Histograms bin把样本分成离散的连续的没有重叠的等间的数据。他们通常用于可视化分散的数值数组。

<a name="histogram" href="#histogram">#</a> d3.<b>histogram</b>() [<>](https://github.com/d3/d3-array/blob/master/src/histogram.js "Source")

Constructs a new histogram generator with the default settings.

构造一个默认参数的直方图生成器。

<a name="_histogram" href="#_histogram">#</a> <i>histogram</i>(<i>data</i>) [<>](https://github.com/d3/d3-array/blob/master/src/histogram.js#L14 "Source")

Computes the histogram for the given array of *data* samples. Returns an array of bins, where each bin is an array containing the associated elements from the input *data*. Thus, the `length` of the bin is the number of elements in that bin. Each bin has two additional attributes:

计算给定数组的直方图。返回直条属性的数组，每个直条都包含输入数据的相关元素。因此，没个直条的长度就是元素的数值，每个直条包括两个属性：

* `x0` - the lower bound of the bin (inclusive).
* `x0` - 直条最小的边界 (包括).
* `x1` - the upper bound of the bin (exclusive, except for the last bin).
* `x1` - 直条最大的边界 (除了最后一个直条，不包括).

<a name="histogram_value" href="#histogram_value">#</a> <i>histogram</i>.<b>value</b>([<i>value</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/histogram.js#L58 "Source")

If *value* is specified, sets the value accessor to the specified function or constant and returns this histogram generator. If *value* is not specified, returns the current value accessor, which defaults to the identity function.

如果指定了 *value*，将数据接收器设置为这个指定的函数或者常量，然后返回一个直方图生成器。如果没有指定 *value*， 返回当前特定函数的数据接收器。

When a histogram is [generated](#_histogram), the value accessor will be invoked for each element in the input data array, being passed the element `d`, the index `i`, and the array `data` as three arguments. The default value accessor assumes that the input data are orderable (comparable), such as numbers or dates. If your data are not, then you should specify an accessor that returns the corresponding orderable value for a given datum.

当一个直方图[生成](#_histogram)了,数据接受器会被应用到输入数组的每个元素，并且传入三个参数元素`d`，索引`i`，数组`data`。默认的数值接收器假定输入数据是有序的（可比较的），比如说数值或日期。如果数据不是可比较的，就必须指定接收器返回给到数据集的顺序。

This is similar to mapping your data to values before invoking the histogram generator, but has the benefit that the input data remains associated with the returned bins, thereby making it easier to access other fields of the data.

这就跟在应用直方图生成器前map处理数据，但是有利于输入的数据与返回的直条保持关联，因此更容易接入其他数据。


<a name="histogram_domain" href="#histogram_domain">#</a> <i>histogram</i>.<b>domain</b>([<i>domain</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/histogram.js#L62 "Source")

If *domain* is specified, sets the domain accessor to the specified function or array and returns this histogram generator. If *domain* is not specified, returns the current domain accessor, which defaults to [extent](#extent). The histogram domain is defined as an array [*min*, *max*], where *min* is the minimum observable value and *max* is the maximum observable value; both values are inclusive. Any value outside of this domain will be ignored when the histogram is [generated](#_histogram).

如果指定了 *domain*，先设置domain接收器设置为指定的函数或数组，然后返回直方图生成器。如果 *domain* 没有指定，返回当前的域接收器，默认为[extent](#extent)。直方图的域是一个数组[*min*, *max*]，*min* 是最小可见数， *max* 是最大可见数，两个都包括在内。直方图[生成[(#_histogram)后任何数值在域之外都会被忽略。

For example, if you are using the the histogram in conjunction with a [linear scale](https://github.com/d3/d3-scale/blob/master/README.md#linear-scales) `x`, you might say:

例如，如果直方图和[线性比例尺](https://github.com/d3/d3-scale/blob/master/README.md#linear-scales) `x`:

```js
var histogram = d3.histogram()
    .domain(x.domain())
    .thresholds(x.ticks(20));
```

You can then compute the bins from an array of numbers like so:

然后从数组numbers计算直方图：

```js
var bins = histogram(numbers);
```

Note that the domain accessor is invoked on the materialized array of [values](#histogram_value), not on the input data array.

注意：域接收器应用到真实的[values](#histogram_value)数组，而不是输入的数组。

<a name="histogram_thresholds" href="#histogram_thresholds">#</a> <i>histogram</i>.<b>thresholds</b>([<i>count</i>]) [<>](https://github.com/d3/d3-array/blob/master/src/histogram.js#L66 "Source")
<br><a name="histogram_thresholds" href="#histogram_thresholds">#</a> <i>histogram</i>.<b>thresholds</b>([<i>thresholds</i>])  [<>](https://github.com/d3/d3-array/blob/master/src/histogram.js#L66 "Source")

If *thresholds* is specified, sets the [threshold generator](#histogram-thresholds) to the specified function or array and returns this histogram generator. If *thresholds* is not specified, returns the current threshold generator, which by default implements [Sturges’ formula](#thresholdSturges). (Thus by default, the histogram values must be numbers!) Thresholds are defined as an array of values [*x0*, *x1*, …]. Any value less than *x0* will be placed in the first bin; any value greater than or equal to *x0* but less than *x1* will be placed in the second bin; and so on. Thus, the [generated histogram](#_histogram) will have *thresholds*.length + 1 bins. See [histogram thresholds](#histogram-thresholds) for more information.

如果指定 *thresholds*, 设置[threshold generator](#histogram-thresholds)为指定的函数或数组，并且返回直方图生成器。如果没指定 *thresholds*，返回当前的阈值生成器，默认是实现[Sturges’ formula](#thresholdSturges)。（因此，默认情况下，直方图的值必须是数值！）。阈值是数组[*x0*, *x1*,...]。数据小于 *x0* 会被放到第一个直方条；大于等于*x0*,小于*x1*的会放到第二个直方条；如此。因此，[generated histogram](#_histogram)会有*thresholds*.length + 1个直方条。查看更多[histogram thresholds](#histogram-thresholds)。

Any threshold values outside the [domain](#histogram_domain) are ignored. The first *bin*.x0 is always equal to the minimum domain value, and the last *bin*.x1 is always equal to the maximum domain value.

直方图会忽略[domain](#histogram_domain)范围之外的阈值。第一个直方条*bin*.x0总是等于最小的domain值，最后一个直方条*bin*.x1总是等于最大的domain值。

If a *count* is specified instead of an array of *thresholds*, then the [domain](#histogram_domain) will be uniformly divided into approximately *count* bins; see [ticks](#ticks).

如果指定 *count*， 而不是 *thresholds*，那么[domain](#histogram_domain)会被分成近似等于 *count* 个直方条；查看[ticks](#ticks)。

### Histogram Thresholds

### 直方图阈值

These functions are typically not used directly; instead, pass them to [*histogram*.thresholds](#histogram_thresholds). You may also implement your own threshold generator taking three arguments: the array of input [*values*](#histogram_value) derived from the data, and the [observable domain](#histogram_domain) represented as *min* and *max*. The generator may then return either the array of numeric thresholds or the *count* of bins; in the latter case the domain is divided uniformly into approximately *count* bins; see [ticks](#ticks).

这些函数通常不直接使用；而是传给[*histogram*.thresholds]。你也可以实现自己的阈值生成器，只需传递三个参数：根据数据而来的输入数组[*values*](#histogram_value), [可见域](#histogram_domain) 的*min* 和 *max*。生成器会返回一个数值阈值的数组或则直方条的*count*。后者domain被等分成近似*count*个直方条。查看[ticks](#ticks)。

<a name="thresholdFreedmanDiaconis" href="#thresholdFreedmanDiaconis">#</a> d3.<b>thresholdFreedmanDiaconis</b>(<i>values</i>, <i>min</i>, <i>max</i>) [<>](https://github.com/d3/d3-array/blob/master/src/threshold/freedmanDiaconis.js "Source")

Returns the number of bins according to the [Freedman–Diaconis rule]
(https://en.wikipedia.org/wiki/Histogram#Mathematical_definition); the input *values* must be numbers.

根据[Freedman–Diaconis rule](https://en.wikipedia.org/wiki/Histogram#Mathematical_definition)返回直方图；输入*values*必须是数值。

<a name="thresholdScott" href="#thresholdScott">#</a> d3.<b>thresholdScott</b>(<i>values</i>, <i>min</i>, <i>max</i>) [<>](https://github.com/d3/d3-array/blob/master/src/threshold/scott.js "Source")

Returns the number of bins according to [Scott’s normal reference rule](https://en.wikipedia.org/wiki/Histogram#Mathematical_definition); the input *values* must be numbers.

根据[Scott’s normal reference rule](https://en.wikipedia.org/wiki/Histogram#Mathematical_definition)返回直方图；输入*values*必须是数值。

<a name="thresholdSturges" href="#thresholdSturges">#</a> d3.<b>thresholdSturges</b>(<i>values</i>) [<>](https://github.com/d3/d3-array/blob/master/src/threshold/sturges.js "Source")

Returns the number of bins according to [Sturges’ formula](https://en.wikipedia.org/wiki/Histogram#Mathematical_definition); the input *values* must be numbers.

根据[Sturges’ formula](https://en.wikipedia.org/wiki/Histogram#Mathematical_definition)返回直方图；输入*values*必须是数值。