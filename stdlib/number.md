---
title: Number对象
layout: page
category: stdlib
date: 2013-03-16
modifiedOn: 2014-01-01
---

Number是数值对应的包装对象，用于生成值为数值的对象。

Number当作工具函数使用时，可以将任何类型的值转为数值。

{% highlight javascript %}

Number(true) // 1

{% endhighlight %}

上面代码将布尔值true转为数值1。

## 属性

Number对象拥有一些特别的属性。

- Number.POSITIVE_INFINITY 表示正的无限，指向关键字Infinity。
- Number.NEGATIVE_INFINITY 表示负的无限，指向-Infinity。
- Number.NaN 表示非数值，指向NaN。
- Number.MAX_VALUE 表示最大的正数，相应的，最小的负数为-Number.MAX_VALUE。
- Number.MIN_VALUE 表示最小的正数（即最接近0的正数，在64位浮点数体系中为5e-324），相应的，最接近0的负数为-Number.MIN_VALUE。

{% highlight javascript %}

Number.POSITIVE_INFINITY // Infinity
Number.NEGATIVE_INFINITY // -Infinity
Number.NaN // NaN
Number.MAX_VALUE // 1.7976931348623157e+308
Number.MIN_VALUE // 5e-324

{% endhighlight %}

## Number实例对象的方法

### toString方法

Number对象部署了单独的toString方法，可以接受一个参数，表示将一个数字转化成某个进制的字符串。

{% highlight javascript %}

(10).toString() // "10"
(10).toString(2) // "1010"
(10).toString(8) // "12"
(10).toString(16) // "a"

{% endhighlight %}

之所以要把10放在括号里，是为了表明10是一个单独的数值，后面的点表示调用对象属性。如果不加括号，这个点会被JavaScript引擎解释成小数点，从而报错。

{% highlight javascript %}

10.toString(2) 
// SyntaxError: Unexpected token ILLEGAL

{% endhighlight %}

但是，在10后面加两个点，JavaScript会把第一个点理解成小数点（即10.0），把第二个点理解成调用对象属性，从而得到正确结果。

{% highlight javascript %}

10..toString(2) 
// "1010"

{% endhighlight %}

这实际上意味着，可以直接对一个小数使用toString方法。

{% highlight javascript %}

10.5.toString() // "10.5"
10.5.toString(2) // "1010.1"
10.5.toString(8) // "12.4"
10.5.toString(16) // "a.8"

{% endhighlight %}

通过方括号运算符也可以调用toString方法。

{% highlight javascript %}

10['toString'](2) // "1010"

{% endhighlight %}

### toFixed方法

toFixed方法用于将一个数转为指定位数的小数。

{% highlight javascript %}

(10).toFixed(2)
// "10.00"
// 10必须放在括号里，否则后面的点运算符会被处理小数点，而不是表示调用对象的方法。

(10.005).toFixed(2)
// "10.01" 

{% endhighlight %}

toFixed的输出支持0到20位小数。

### toExponential方法

toExponential方法用于将一个数转为科学计数法形式。

{% highlight javascript %}

(10).toExponential(1)
// "1.0e+1"

(1234).toExponential(1)
// "1.2e+3"

{% endhighlight %}

toExponential方法的参数表示小数点后有效数字的位数。

### toPrecision方法

toPrecision方法用于将一个数转为指定位数的有效数字。

{% highlight javascript %}

(12.34).toPrecision(1)
// "1e+1"

(12.34).toPrecision(2)
// "12"

(12.34).toPrecision(3)
// "12.3"

(12.34).toPrecision(4)
// "12.34"

(12.34).toPrecision(5)
// "12.340"

{% endhighlight %}

toPrecision方法提供的有效数字位数的范围是1到21。

toPrecision方法用于四舍五入时不太可靠，可能跟浮点数不是精确储存有关。

{% highlight javascript %}

(12.35).toPrecision(3)
// "12.3"

(12.25).toPrecision(3)
// "12.3"

(12.15).toPrecision(3)
// "12.2"

(12.45).toPrecision(3)
// "12.4"

{% endhighlight %}
