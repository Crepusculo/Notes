<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [FLEX](#flex)
   - [除此之外, 还有](#除此之外-还有)
   - [`justify-content`](#justify-content)
      - [order](#order)
   - [容器内部](#容器内部)
      - [`order`](#order)
      - [`flex-grow`](#flex-grow)
      - [`flex-shrink`](#flex-shrink)
      - [`flex-basis`](#flex-basis)
      - [`flex`](#flex)
      - [`align-self`](#align-self)
- [Trap * Trick](#trap-trick)
   - [flex 内部模型](#flex-内部模型)
   - [Lab](#lab)
- [Other display mode](#other-display-mode)
   - [<div class="green">display-outside</div>](#div-classgreendisplay-outsidediv)
   - [<div class="green">display-inside</div>](#div-classgreendisplay-insidediv)
   - [<div class="green">display-listitem</div>](#div-classgreendisplay-listitemdiv)
   - [<div class="green">display-internal</div>](#div-classgreendisplay-internaldiv)
   - [SYNTAX](#syntax)
- [Yet another Trap & Trcik](#yet-another-trap-trcik)

<!-- /MDTOC -->
# FLEX

`display:flex`
`display:inline-flex`

main-axis 指横着的轴
cross-axis 指竖轴

main-size 指容器内元素的横宽度
cross-size 指容器内元素的竖宽度

## 除此之外, 还有

+ `justify-content` 主轴上的对齐方式
    + `flex-start` 从main-start轴开始对齐
    + `flex-end` 从main-end轴开始对齐
    + `center` 居中
    + `space-between` 两端对齐
    + `space-around` 均匀布局
+ `align-items` 侧轴
    + 定义 flex: 的子元素在 flex 容器的**当前行**的侧轴(cross-axis)(y-axis)方向上的对齐方式
    + `stretch`==[默认值]==
    + `center`
    + `flex-start`
    + `flex-end`
    + `baseline`基线
    + `initial`
    + `inherit`继承父级
+ `align-content` 属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
    + `stretch`==[默认值]==
    + 多根轴线相对于正交轴如何分布的问题, 表现形式和`justify-content`基本相同
+ `flex-direction`顾名思义, 子元素的展开方向
    + `row`==[default]== |  `row-reverse` | `column` | `column-reverse`
    + 左和上为正
+ `flex-wrap`
    + 定义 flex: 容器的元素在排列空间不够时采取的行动
    + `nowrap` 不换行, 多余的元素被挤出显示区域
    + `warp`第一行排满后 向排列方向 创建新行
    + `warp-reverse`第一行排满后 向排列方向移动, 在移开的位置用新行填充
+ `flex-flow`
    + 简写属性 语法为`<flex-direction> || <flex-wrap>;`



## `justify-content`
https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content

+ justify-content 作用于 main-axis
+ 对于flex和非flex都起作用, 但是有不同的执行参数
    + flex-start | flex-end
    + start | end
    + center

https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content#result

### order
[stackoverflow e.g.](http://stackoverflow.com/questions/32991051/absolutely-positioned-flex-item-not-being-removed-from-normal-flow-in-firefox)

## 容器内部
### `order`
序号, 支持负数

### `flex-grow`
放大系数, 默认为0 表示不放大
如果所有项目的`flex-grow`属性都为 1，则它们将等分剩余空间（如果有的话）。
如果一个项目的`flex-grow`属性为 2，其他项目都为 1，则前者占据的剩余空间将比其他项多一倍。
### `flex-shrink`
缩小比例
如果所有项目的`flex-shrink`属性都为 1，当空间不足时，都将等比例缩小。
如果一个项目的`flex-shrink`属性为 0，其他项目都为 1，则空间不足时，前者不缩小。
### `flex-basis`
属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。

这是一个长度值, 可以为 auto

### `flex`
上面这三个的简写属性
```
flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
```

flex:auto -> 1 1 auto
flex:none -> 0 0 auto

### `align-self`
`align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。

取值和 `align-items` 的6个可选值一样

---------

# Trap * Trick
+ 阮一峰的博客已经过时了, 在 chrome29+ 以后已经不再需要 `-webkit-` 前缀
----------
+ `display:flex` 和 `flex` 是两个东西, 某种意义上, 是父子关系
---------
+ 弹性容器直接包含的文本将自动包覆成匿名弹性项目。
    + 不过, 一个只包含一系列空白符（如一堆空格或制表符等）的匿名弹性项目不会被渲染，就如同对其指派 display: none。
-------
+ 相邻的弹性元素其外边距不会互相合并。
    + 使用 auto 外边距可以吸收掉水平或垂直方向上的额外空间，这可以用于对齐或分隔相邻的弹性项目。
------
+ 元素的显示顺序与它们在源代码中的顺序无关，这种无关性只影响视觉呈现，语音顺序以及基于源代码顺序的导航均不受影响。
-------
+  `float` `clear` `vertical-align` 属性将失效
+ 由于弹性盒子使用了不同的布局算法，某些属性用在弹性容器上没有意义：
    + 多栏布局模块的 column-* 属性对弹性项目无效。
    + float 与 clear 对弹性项目无效。使用 float 将使元素的 + display 属性计为block。
    + vertical-align 对弹性项目的对齐无效。

-------

## flex 内部模型
+  `flex`的所有的子元素都是这个`flex`容器的成员
> Each in-flow child of a flex container becomes a flex item.

+ 是成为成员, 而不是继承属性

重点是伪元素也会这样。

回忆一下在chrome下的一个小例子::
```html
<!-- pseudo class render class -->
<div>
    ::before
    <p></p>
    ::after
</div>
```
然后上面这个就变成了一个 before - p - after 顺序的flow

这个bug在 Firefox 文档中专门被标记(bug 857454)
https://developer.mozilla.org/en-US/Firefox/Releases/23#CSS
(干他妈的)

我们依然可以通过将 pseudo-element 设置为 absolute 从而将其从正常流中删除, 但是这种方法在有的浏览器中并没有什么卵用

## Lab
http://demo.agektmr.com/flexbox/
http://the-echoplex.net/flexyboxes
http://codepen.io/justd/pen/yydezN


# Other display mode

https://developer.mozilla.org/en-US/docs/Web/CSS/display

## <div class="green">display-outside</div>
These keywords specify the element’s outer display type, which is essentially its role in flow layout. They are defined as follows:

+ <span class='green m'>block</span> 开始新的一行, 并且尽可能撑满容器
    + div, section, header, footer ...
    + here is our test<div class="html">foo</div>
+ <span class='green m'>inline</span>行内元素, 不打断段落的布局
    + a 是最常用的行内元素
    + 另一个常见的例子是 span
    + here is our test<a class="html">foo</a>
+ <span class='green m'>run-in</span>==lab==
    + 根据上下文
    + 内含 block 变成 block
    + 在 block 前会变为 block 的第一次个 inline box
    + 在 inline 前 变成 block box

## <div class="green">display-inside</div>
These keywords specify the element’s inner display type, which defines the type of formatting context that lays out its contents (assuming it is a non-replaced element). They are defined as follows:

+ <span class='green m'>flow</span>==lab==If its outer display type is inline or run-in, and it is participating in a block or inline formatting context, then it generates an inline box. Otherwise it generates a block container box.

+ <span class='green m'>flow-root</span>==lab==
+ <span class='green m'>table</span> These elements behave like `<table>` HTML elements. It defines a block-level box.
+ <span class='green m'>flex</span>
+ <span class='green m'>grid</span>	The element behaves like a block element and lays out its content according to the grid model.
+ <span class='green m'>subgrid</span>==lab==	If the parent element has `display:grid`, the element itself and its content are laid out according to the grid model.
+ <span class='green m'>ruby</span>==lab==
    + It behaves like the corresponding `<ruby>` HTML elements.
    + 就是注音那个破玩意儿
## <div class="green">display-listitem</div>

The element generates a block box for the content and a separate list-item inline box.

If no `<display-inside>` value is specified, the principal box’s inner display type defaults to `flow`.

If no `<display-outside>` value is specified, the principal box’s outer display type defaults to `block`.

## <div class="green">display-internal</div>

某些标签, 比如`ruby`和`table`这样的, 内部的标签有自己专门的display规则
具体的还是去看
https://developer.mozilla.org/en-US/docs/Web/CSS/display#display-internal
吧

<div class="green">display-box</div>
These values define whether an element generates display boxes at all.

+ <span class='green m'>none</span>
    + 用来在不删除元素的情况下隐藏或显示元素。
    + 有一些元素默认就是 `display:none` 的, 比如 script
    + 一个看不见的例子<a style="display:none">2333</a>
+ <span class='green m'>contents</span>==lab==
    + 不产生一个特定的盒模型 只是拿来和`none`作区分

<div class="green">display-legacy</div>

A single-keyword example
```
inline-block
```

在 CSS 2 年代, 这群人使用 single-keyword 句法来描述 display 属性。
CSS 3 里他们吃书了, 觉得 display 也应该是可以拆的

https://developer.mozilla.org/en-US/docs/Web/CSS/display#display-legacy

## SYNTAX
```
[ <display-outside> || <display-inside> ] | <display-listitem> | <display-internal> | <display-box> | <display-legacy>
```

# Yet another Trap & Trcik

+ 尽管上文中出现了 `display:flow` 这种东西, 但是不管是 google 还是 MDN 的兼容性列表, 这种东西都根本没出现过
