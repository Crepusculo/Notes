<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [三层盒模型](#三层盒模型)
- [box-shadow](#box-shadow)
   - [box-shadow 多重边框](#box-shadow-多重边框)
   - [box-shadow + outline 双层边框](#box-shadow-outline-双层边框)
- [background](#background)
   - [background](#background)
   - [background 多重背景详解](#background-多重背景详解)
   - [background-blend-mode](#background-blend-mode)
- [盒模型的边和角的值简写语法](#盒模型的边和角的值简写语法)
- [渐变与条纹](#渐变与条纹)
   - [SVG vs. CSS](#svg-vs-css)
- [border](#border)
   - [border-image 连续的图像边框](#border-image-连续的图像边框)
      - [border-image 与 九宫格伸缩法](#border-image-与-九宫格伸缩法)
      - [border-image-slice](#border-image-slice)
      - [Formal Syntax](#formal-syntax)
      - [作为保险的补充 不清真的做法](#作为保险的补充-不清真的做法)
- [Tricks](#tricks)
   - [伪随机背景 [条纹渐变][多重背景]](#伪随机背景-条纹渐变多重背景)
   - [图片背景叠底的多种实现方式](#图片背景叠底的多种实现方式)

<!-- /MDTOC -->

# 三层盒模型
`content-box` - `padding-box` - `border-box`

<a style="background:teal; color:teal;">...</a>outline 5px
<a style="background:#ff4; color:#ff4;">...</a>border 50px (hide due to border-image
<a style="background:#7ce; color:#7ce;">...</a>shadow 20px default
<a style="background:#655; color:#655;">...</a>shadow 15px default
<a style="background:teal;color:teal;">...</a>shadow 15px inset
<a style="background:url('https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcSrqAE1wNfyd4Sygtzlk7AHvLK7rGoEqo7efJbv2cGbOLejaEIhrA');color:green;">...</a>border-image: 50px (outset:25px)
<a style="background:#fb3;"> 100px </a>border-box
<a style="background:#fb3;"> 20px </a>padding-box
<a style="background:#fb3;"> 10px </a>content-box

<div class="html">
<div style="width:600px; height:400px; margin:0 auto; padding:100px;
  outline: 5px dotted;
  border-radius:50px;
  box-shadow: 0 0 0 15px #655,
               0 0 0 20px #7ce,
               0 0 0 15px teal inset;
  background: repeating-linear-gradient(45deg,
               #fb3, #fb3 20px, transparent 0,transparent 100px),
               repeating-linear-gradient(45deg, #fb3, #fb3 10px, transparent 0,transparent 20px),               repeating-linear-gradient(45deg,
               #fb3, #fb3 5px, transparent 0,transparent 10px);
  background-clip: border-box,padding-box,content-box;
  border: 50px dashed #ff4;
  border-image-source:url('https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcSrqAE1wNfyd4Sygtzlk7AHvLK7rGoEqo7efJbv2cGbOLejaEIhrA');
  border-image-width:50px;
  border-image-slice:33% 33%;
  border-image-outset:25px;
  border-image-repeat:round;
">Content-box
</div>
</div>

+ 盒模型有三层主结构
+ 但是 `box-sizing` 只有 `border-box`和`content-box`两个属性


# box-shadow

+ box-shadow 本来的作用是生成投影
+ 与 border 相比, box-shadow 最大的好处是可以生成任意数量的投影来模拟边框
+ box-shadow 层层叠加的方式是第一层位于层顶, 其后每一层位于下方
    + 其宽度是从边框算起的半径, 而不是从上一层 box-shadow 算起
+ 投影的行为和边框**不完全一致**
    + 投影不影响布局
    + 投影不受到 box-sizing 的影响
    + 投影始终贴合border线
+ 正常box-shadow贴合 border 外边界, offset-box-shadow 贴合内边界
+ 用投影做出的虚假边框出现在元素的**外圈**,它们并不会响应鼠标事件。

## box-shadow 多重边框
<div class="html">
 <div style="width:300px; height:200px; margin:0 auto;
   box-shadow: 0 0 0 10px #655,
               0 0 0 15px teal;
   background: repeating-linear-gradient(45deg,
               #332121, #332121 15px, #212121 0,#212121 30px);
">

两个外层 box-shadow叠加
外层宽度 = 15px - 10px = 5px
</div>
</div>
<div class="html">
<div style="width:300px; height:200px; margin:0 auto;
 box-shadow: 0 0 0 10px #655 inset,
             0 0 0 15px #fb3 ;
 background: repeating-linear-gradient(45deg,
             #332121, #332121 15px, #212121 0,#212121 30px);
">灰色往里扩展了
</div>
</div>

## box-shadow + outline 双层边框
一幅图说明 `outline` 和 `box-shadow` 的不同
<div class="html">
<div style="width:300px; height:200px; margin:0 auto;
  outline: 5px solid;
  border-radius:32px;
  box-shadow: 0 0 0 10px #655 inset,
              0 0 0 15px teal ;
  background: repeating-linear-gradient(45deg,
              #fb3, #fb3 15px, transparent 0,transparent 30px);
">
</div>
</div>

# outline
+ `outline` 不接受多个值
+ `outline` 作用于border-content盒模型外边, 但是不会贴合border-content盒模型
+ `outline` 可以接受一个负值
+ `outline` 骑 border 外边界的脸

# background

| |  |
|--|--
| background-color |
| background-position |
| background-size |
| background-repeat | `repeat` `repeat-x` `repeat-y` `no-repeat` `inherit`
| background-origin|
| background-clip |
| background-attachment| `scroll`or`fixed` |
| background-image |



```css
background: [background-color] [background-image] [background-repeat] [background-attachment]
        [background-position] / [background-size]
        [background-origin] [background-clip];
        /// 除了background,font和border-radius也有简写 ///
```



## background

## background 多重背景详解
`background` 属性和`box-shadow`一样 可以制造多层背景
+ 层叠顺序为从前到后

<div class="html">
<div style="margin:auto;
    width:400px; height:400px;
    background-image:
        linear-gradient(45deg, yellow 42px, red 0),
        repeating-linear-gradient(45deg,
                  #fb3, #fb3 15px, transparent 0,transparent 30px),
        repeating-linear-gradient(135deg,
                  #e2b, #e2b 15px, transparent 0,transparent 30px);
    background-size:100px 100px, 100% 100%, 100%  100%;
    background-repeat:no-repeat;
    background-position:right 100px bottom 10px,0 0,right 100px bottom 100px;
">
</div>
</div>

## background-blend-mode

# 盒模型的边和角的值简写语法
https://developer.mozilla.org/zh-CN/docs/Web/CSS/Shorthand_properties#Background_Properties

简单来说
对于盒的边 顺序是 `上 右 下 左` 以上为起点的顺时针
```
a       -> a a a a
a b     -> a b a b
a b c   -> a b c b
a b c d -> a b c d
```
对于角来说 顺序是 `左上 右上 右下 左下` 的顺时针
```
a       -> a a
           a a

a b     -> a b
           b a

a b c   -> a b
           b c

a b c d -> a b
           d c
```

# 渐变与条纹

渐变 color a ->color b 的本质是划定两端, 中间根据算法填充 的一幅 `<image>`
如果出现 a b 重合的情况 会出现一条明显的分界线

要记住, 渐变的实质是产生的 background-image

<table>
<tr><td><div class="mbox  mono black" style="
background:linear-gradient(90deg, red 0, white 100%);">
0-100%
</div></td>
<td><div class="mbox  mono black" style="
background:linear-gradient(90deg, red 40%, white 60%);">
40%-60%
</div></td>
<td><div class="mbox  mono black" style="
background:linear-gradient(90deg, red 50%, white 50%);">
50%-50%
</div></td>
</tr>
<tr><td><div class="mbox  mono black" style="
background:linear-gradient(45deg, red 0, white 100%);
background-size:50% 50%; background-repeat:repeat;">
0-100% 45deg <br>
50% 50% repeat
</div></td>
<td><div class="mbox  mono" style="
background:linear-gradient(45deg, red 0, white 100%);
background-size:80% 20%; background-repeat:no-repeat;">
0-100% 45deg 80% 20% <br> no-repeat
</div></td>
<td><div class="mbox  mono" style="
background:linear-gradient(45deg, red 0, white 100%);
background-size:20% 80%; background-repeat:no-repeat;">
0-100% 45deg 20% 80% <br> no-repeat
</div></td>
</tr>
</table>

如上面涉及到的, 我们可以利用 重合的颜色线来画出条纹线


<table>
<tr><td><div class="mbox black mono" style="
background:linear-gradient(45deg, red 50%, white 0);
 background-repeat:no-repeat;">
50%-0 45deg 100% 100%
</div></td>
<td><div class="mbox  mono black" style="
background:linear-gradient(45deg, red 50%, white 0);
background-size:50% 50%; background-repeat:repeat;">
50%-0 45deg 50% 50% <br> repeat
</div></td>
<td><div class="mbox mono black" style="
background:linear-gradient(45deg, red 50%, white 0);
background-size:100% 50%; background-repeat:repeat;">
50%-0 45deg 100% 50% <br> repeat
</div></td>
</tr>
<tr><td><div class="mbox mono black s" style=" text-align:center;
background:linear-gradient(45deg, #48a 25%, #fba 0, #fba 50%, #48a 0, #48a 75%, #fba 0);
background-size:100% 100%; background-repeat:repeat;">
25%-0-50%-0-75%-0<br>
蓝-粉-粉-蓝-蓝-粉<br>
45deg 100% 100% <br>
</div></td>
<td><div class="mbox mono black s" style=" text-align:center;
background:linear-gradient(45deg, #48a 25%, #fba 0, #fba 50%, #48a 0, #48a 75%, #fba 0);
background-size:50% 50%; background-repeat:repeat;">
25%-0-50%-0-75%-0<br>
蓝-粉-粉-蓝-蓝-粉<br>
45deg 50% 50% <br> repeat
</div></td>
<td><div class="mbox mono black s" style=" text-align:center;
background:linear-gradient(45deg, #48a 25%, #fba 0, #fba 50%, #48a 0, #48a 75%, #fba 0);
background-size:25% 25%; background-repeat:repeat;">
25%-0-50%-0-75%-0<br>
蓝-粉-粉-蓝-蓝-粉<br>
45deg 25% 25% <br> repeat
</div></td></tr>
<tr><td><div class="mbox mono black s" style="
background:linear-gradient(45deg, #e8a 25%, #fea 0, #fea 50%, #48a 0, #48a 75%, #fba 0);
background-size:50% 50%; background-repeat:repeat;">
其实是由 <br>
[粉 - 黄 - 蓝 - 红]
这样的四块
拼合而成
</div></td>
<td><div class="mbox mono black s" style=" text-align:center;
background:linear-gradient(45deg, #48a 10%, #fba 0, #fba 50%, #48a 0, #48a 70%, #fba 0);
background-size:25% 25%; background-repeat:repeat;">
当然 也可以不是等宽
10%-0-50%-0-70%-0<br>
蓝-粉-粉-蓝-蓝-粉<br>
</div></td>
<td><div class="mbox mono black s" style=" text-align:start;
background:linear-gradient(60deg, #48a 25%, #fba 0, #fba 50%, #48a 0, #48a 75%, #fba 0);
background-size:50% 50%; background-repeat:repeat;">
这种"类似贴片"方法
有很大局限性
特别是在值不好计算时<br>
(换句话话, 只有在 0, 45, 90 比较好用)<br>
图中为 60deg 的情况
</div></td></tr>
<tr>
<td colspan="2"><div class="mono black s" style="text-align:start;
background:repeating-linear-gradient(60deg, #48a 25%, #fba 0, #fba 50%, #48a 0, #48a 75%);">
使用 repeating-linear-gradient, </br>
替代 linear-gradient, </br>
创建更简单和灵活的重复条纹 </br>
这时候长度值是基于渐变轴直接计算的 </br>
25%-0-50%-0-75%
</div></td>
<td><div class="mbox mono black s" style="text-align:start;
background:repeating-linear-gradient(60deg, #48a, #48a 25px, #fba 0, #fba 50px);">
background:repeating-linear-gradient (60deg, #48a, #48a 15px, #fba 0, #fba 30px);
</div></td></tr>
<tr><td><div class="mbox mono black s" style="text-align:start;
background:repeating-linear-gradient(45deg, #48a, #48a 25%, #fba 0, #fba 50%);
background-size: 25% 25%">
在创建45° 的条纹贴片时
我们甚至可以混合两种方法
来减少代码量
<td><div class="mbox mono black s" style="text-align:start;
background:#58a;
background-image:repeating-linear-gradient(45deg, transparent, transparent 15px, hsla(0,0%,100%,0.1) 0, hsla(0,0%,100%,0.1) 30px);
">

</div></td>
</div></td></tr></table>

在不使用 sass 等工具的情况下, 条纹的代码量其实是蛮大的, 而且很不 dry, 通常, 你要修改一个颜色或宽度 需要修改多个地方,

对于同色系来说, 我们可以使用半透明条纹覆盖在纯色背景上来解决这个问题, 在这种情况下, 我们仅仅需要改变一处颜色即可
## SVG vs. CSS

+ CSS 渐变 可以节省掉 HTTP 请求
    + 但是对于现代浏览器来说, 我们可以把 SVG 文件 以 data URI 的方式内嵌到样式表中, 甚至不需要用 base64 或 URLencode 来对其编码:
    + ```css
        background: #eee url('data:image/svg+xml,\
                    <svg xmlns="http://www.w3.org/2000/svg"\
                    width="100" height="100" \
                    fill-opacity=".25">\
                    <rect x="50" width="50" height="50" /> \
                    <rect ="50" width="50" height="50" /> \
                    </svg>');
        background-size: 30px 30px;
        ```
        http://play.csssecrets.io/checkerboard-svg
+ SVG 代码量更小
+ SVG 代码冗余方面也更好, 通常只需要更改一两个地方即可

# border

## border-image 连续的图像边框
+ border-image 最大的问题在于 "没有人一定要让图片的"
### border-image 与 九宫格伸缩法

border-image 也是简写属性

`border-image: source slice width outset repeat |initial|inherit;`

_`source`_:
_`slice`_:How to slice the border image 九宫格如何划分
_`width`_:边框宽度
_`outset`_:边框图像区域超出边框的量
_`repeat`_:图像边框是否应平铺 (repeated)、铺满 (rounded) 或拉伸 (stretched)。
round-stretch

[W3S Sample](https://www.w3schools.com/cssref/tryit.asp?filename=trycss3_border-image)


### border-image-slice
![Slice](https://developer.mozilla.org/files/3814/border-image-slice.png)
<style>
.border-image-slice{
    border: 50px solid transparent;
    border-image-source:url('https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcSrqAE1wNfyd4Sygtzlk7AHvLK7rGoEqo7efJbv2cGbOLejaEIhrA');
    border-image-width: 1;
}
</style>

<table><tr><td><div class="mbox mono border-image-slice" style="
border-image-slice: 20%;
">slice:20%</div></td>
<td><div class="mbox mono border-image-slice" style="
border-image-slice: 33%;
">slice:33%</div></td>
<td><div class="mbox mono border-image-slice" style="
border-image-slice: 50%;
">slice:50%</div></td>
</tr>
<tr><td><div class="mbox mono  border-image-slice" style="
border-image-slice: 51%;
">slice:51%</div></td>
<td><div class="mbox mono border-image-slice" style="
border-image-slice: 100%;
">slice:100%(initial)</div></td>
<td><div class="mbox mono border-image-slice" style="
border-image-slice: 112;
">slice:112</div></td>
</tr>
<tr><td><div class="mbox mono border-image-slice" style="
border-image-slice: 33% 100%;
">slice: 33% 100%</div></td>
<td><div class="mbox mono border-image-slice" style="
border-image-slice: 51% 50%;
">slice: <br>51% 50%</div></td>
<td><div class="mbox mono border-image-slice" style="
border-image-slice: unset;
">slice: unset</div></td>
</tr>
<tr><td><div class="mbox mono border-image-slice" style="
border-image-slice: 5% 33% 50%;
">slice: 5% 33% 50%</div></td>
<td><div class="mbox mono border-image-slice" style="
border-image-slice: 33% 5% 33% 50%;
">slice: <br>33% 5% 33% 50%</div></td>
<td><div class="mbox mono border-image-slice" style="
border-image-slice: 10 20% 60% 70% fill;
">slice: <br>10 20% 60% 70% fill</div></td>
</tr>
<tr><td><div class="mbox mono border-image-slice" style="
border-image-slice: 33% fill;
">slice: 33% fill</div></td>
<td><div class="mbox mono border-image-slice" style="
border-image-slice: 10% fill ;
">slice: <br>10% fill</div></td>
<td><div class="mbox mono border-image-slice" style="
border-image-slice: 10% 33% fill;
">slice: 10% 33% fill</div></td>
</tr>
</table>

Syntax

```css
/* border-image-slice: slice */
border-image-slice: 30%;

/* border-image-slice: vertical horizontal */
border-image-slice: 10% 30%;

/* border-image-slice: top horizontal bottom */
border-image-slice: 30 30% 45;

/* border-image-slice: top right bottom left */
border-image-slice: 7 12 14 5;

/* border-image-slice: … fill */
/* The fill value can be placed between any value */
border-image-slice: 10% fill 7 12;
/* 这条不行, 至少在Electron里不行 */

/* Global values */
border-image-slice: inherit;
border-image-slice: initial;
border-image-slice: unset;
/**/
```

硬要解释一波的话:
每个值代表的是: 这个部分由原图的 "多少" 来组成, 比如
`33%` 代表4个角落都是 33% * 33% 组成的
`10% 50 33%` 代表4个角落分别是: 10% * 50px, 10% * 50px, 33% * 50px, 33% * 50px

所以在 `51%`的时候中间一截会丢失: 51%+51% = 102%
中间一截代表在原图中的大小是 100%-102% = -2%
自然就无法显示了
但是注意, 负数无法显示, 但是 0 是可以的

fill 表示中间一格是否填充

border-image 的宽度由 border 属性本身决定

### Formal Syntax
```
    <number-percentage>{1,4} && fill?
    where
    <number-percentage> = <number> | <percentage>
```

使用 number 的话,代表 pixel

### 作为保险的补充 不清真的做法

# Tricks
## 伪随机背景 [条纹渐变][多重背景]
+ 当用户注意到重复背景上一个有辨识度的特征(找到重复规律), 那么营造的随机性就不复存在
+ 模拟随机条纹 = 多个条纹背景叠加
+ 最上层的贴片 没有任何贴片为其提供遮挡 其重复性最容易被发现
    + 所以最上层的贴片应该最长
    + 我们应该把平铺间距最大的贴片安排在最上面
+ 最短重复尺寸是每个单色条纹的最小公倍数
    + 比如一个 background-size: 80 60 40 的三重贴片组, 其重复的间距是其最小公约数是 240
    + 所以我们因为选质数
    + 一个 41 61 83 的贴片组, 重复间距是 207583 像素
    + 这个问题其实没那么简单, 有时候差那么几个像素看起来也差不多
    + 再次强调, bk-image 的覆盖顺序是从上到下
<div class="html">
<div style=" height:200px;
  background:hsl(20,40%,90%);
  background-image:
    linear-gradient(90deg,#fb3 10px,transparent 0),
    linear-gradient(90deg,#3b7 10px,transparent 0),
    linear-gradient(90deg,#444 15px,transparent 0),
    linear-gradient(90deg,#b73 20px,transparent 0);
  background-size: 131px 100%,61px 100%,41px 100%;
    ">c</div>
</div>

+ 质数模仿非重复这种技巧被称为蝉原则, 由 Alex Walker 提出。
    + 其他用处:
    + 一个不想让人看出在按明显规律在循环重复的动画
    + 在照片图库中通过 :nth-child(a) 中 a 为质数,使每张照片应用旋转的度数

## 图片背景叠底的多种实现方式
1. 两个元素, 一个略大的作为背景, 一个略小的覆盖在其上,作为底板
<div class="html">
<div id="#bk" style="padding:48px; height:330px;
background:url('http://lorempixel.com/500/330/food')">
<div style="padding:12px;
background:rgba(12,12,12,0.7)
">

+ 结构和表现混合起来
+ 需要修改 HTML
+ 但是简单
+ 背景格式是 background, 自由度相对还不错
+ 高度自适应
+ 垂直居中需要单独设置, 比如现在这样


</div></div></div>

2. border-image + background
`border-image: source slice width outset repeat;`
<div class="html">
<div id="#bk" style="padding:24px;height:330px;
background:rgba(121,12,12,0.8);
border: 48px solid transparent;
border-image-source:url('http://lorempixel.com/500/330/food');
border-image-slice:10%;
border-image-width:48px;
">

+ border-image 层实际上在 background 层的上面
+ 没办法做半透明,slice 开 fill 试试
+ 难维护, 比如这个地方和上面没对齐的原因是border width 有48px, 又比如图片大小和结构耦合写死了
+ 图片的四个角一定对应四个盒模型的四个边角 是个伪需求 是阴谋论 是阿共搞的鬼
</div></div>

3. multiple-background

<div class="html">
<div id="#bk" style="padding:24px;height:330px;
background:
linear-gradient(135deg,rgba(21,21,21,0.9) 90%,transparent 0) no-repeat,url('http://lorempixel.com/500/330/food');
background-size:85%,100%;
background-position:center;
">

+ 最大的缺点如你所见, 这个方法需要手工校对第一个作为文字底板的 background-iamge 和 padding 的相对距离
+ 并且这个问题会延伸到响应式中
+ 不过这样方法有半透明, 还可以完美居中
+ 这不是最完美的多重背景实现
</div></div>

4. advance-multiple-background
<div class="html">
<div id="#bk" style="padding:24px; height:330px;
border: 24px solid transparent;
background:
linear-gradient(135deg,rgba(21,21,21,0.9) 90%,transparent 0) no-repeat,url('http://lorempixel.com/500/330/food');
background-clip:padding-box,border-box;
background-position:center;
">

+ 利用透明 border 扩展盒模型
+ 利用盒模型 clip 属性自动留白, 使用 background-clip 替代 background-size 避免手工操作
+ 不过在这个模型中, 要记住额外的外层图像内容是在 border 下的
</div></div>
