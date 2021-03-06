<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [三层盒模型](#三层盒模型)   
- [box-shadow](#box-shadow)   
   - [关于如何投影你想要的投影](#关于如何投影你想要的投影)   
   - [box-shadow 多重边框](#box-shadow-多重边框)   
   - [box-shadow + outline 双层边框](#box-shadow-outline-双层边框)   
- [outline](#outline)   
- [background](#background)   
   - [background](#background)   
   - [background 多重背景详解](#background-多重背景详解)   
   - [background-blend-mode](#background-blend-mode)   
- [盒模型的边和角的值简写语法](#盒模型的边和角的值简写语法)   
- [渐变与条纹](#渐变与条纹)   
   - [SVG vs. CSS](#svg-vs-css)   
- [border](#border)   
- [border-image](#border-image)   
   - [border-image 连续的图像边框](#border-image-连续的图像边框)   
      - [border-image 与 九宫格伸缩法](#border-image-与-九宫格伸缩法)   
      - [border-image-slice](#border-image-slice)   
         - [Formal Syntax](#formal-syntax)   
      - [border-image-repeat](#border-image-repeat)   
      - [border-image-width](#border-image-width)   
      - [border-image-outset](#border-image-outset)   
- [border-radius](#border-radius)   

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

```
参数
box-shadow: [水平偏移量] [垂直偏移量] [模糊半径] [向外扩张的程度] [颜色]
```

## 关于如何投影你想要的投影
http://www.corelangs.com/css/box/shadow.html

## box-shadow 多重边框
 <div style="width:300px; height:200px; margin:0 auto;
   box-shadow: 0 0 0 10px #655,
               0 0 0 15px teal;
   background: repeating-linear-gradient(45deg,
               #332121, #332121 15px, #212121 0,#212121 30px);
">

两个外层 box-shadow叠加
外层宽度 = 15px - 10px = 5px

</div>
<div style="width:300px; height:200px; margin:0 auto;
 box-shadow: 0 0 0 10px #655 inset,
             0 0 0 15px #fb3 ;
 background: repeating-linear-gradient(45deg,
             #332121, #332121 15px, #212121 0,#212121 30px);
">

灰色往里扩展了
此外我们可以注意到, box-shadow遮盖了一部分上一个元素
</div>

## box-shadow + outline 双层边框
一幅图说明 `outline` 和 `box-shadow` 的不同
<div style="width:300px; height:200px; margin:0 auto;
  outline: 5px solid;
  border-radius:32px;
  box-shadow: 0 0 0 10px #655 inset,
              0 0 0 15px teal ;
  background: repeating-linear-gradient(45deg,
              #fb3, #fb3 15px, transparent 0,transparent 30px);
">
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
                  #efb, #efb 15px, transparent 0,transparent 30px);
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
look at this border<span class="sbox" style="
    border:24px solid transparent;
    border-top-color: #fb8;
    border-left-color: #009688;
    border-right-color: #83aafe;
    border-bottom-color: #b44;
">text
</span>
<div style=" height:100px; width:100px;
    border:24px solid transparent;
    border-top-color: #fb8;
    border-left-color: #009688;
    border-right-color: #83aafe;
    border-bottom-color: #b44;
">test
</div>
border 从盒模型的 border-box 边界向内扩张


+ border 的 right 在 inline 模式下通常会被截断导致你看不完整

# border-image
## border-image 连续的图像边框
+ border-image 最大的问题在于 "没有人一定要让图片的4个边角对应盒模型的四个边角"
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

#### Formal Syntax
```
    <number-percentage>{1,4} && fill?
    where
    <number-percentage> = <number> | <percentage>
```

使用 number 的话,代表 pixel　__(图片像素而不是屏幕像素)__

### border-image-repeat
### border-image-width
### border-image-outset

# border-radius
```
border-radius: [四个角]
border-radius: [左上右下] [右上左下]
...

border-radius: [纵向] / [径向]
```

![](https://user-gold-cdn.xitu.io/2017/5/19/a7dc1c4612749412a1d6f2337ee13af0)
半径画出的圆遭遇任一另一个边界圆时都会停止扩张

> 当任意两个相邻圆角的半径之和超过 border box 的尺寸时, 用户代理必须按比例缩小各个边框半径所使用的值, 直到它们不会相交为止
> ------ <cite>w3.org</cite>

( 所以 100% 50% 这种其实是被压缩到了 50% 25% )
注意 : 100% / 50% 的缩小程度还没到 50% / 25%
<table>
<tbody>
        <tr>
            <td><section class="sbox mono black" style="border-radius:40px">40px</section></td>
            <td><section class="sbox mono black" style="border-radius:40px 20px">40px 20px</section></td>
            <td><section class="sbox mono black" style="border-radius:40px 30px 20px ">40px 30px 20px</section></td>
            <td><section class="sbox mono black" style="border-radius:40px 30px 20px 10px ">40px 30px 20px 10px</section></td>
        </tr>
</tbody>
</table>

<table>
<tbody>
        <tr row="1">
            <td><section class="mbox-e mono black" style="border-radius:45%">45%
            </section></td>
            <td><section class="mbox-e mono black" style="border-radius:50%">50% </section></td>
            <td><section class="mbox-e mono black" style="border-radius:999px">999px
            </section></td>
        </tr>
        <tr  row="2">
            <td><section class="mbox-e mono black" style="border-radius:100% 50%">100% 50%
            </section></td>
            <td><section class="mbox-e mono black" style="border-radius:50% 25%">50% 25%; </section></td>
            <td><section class="mbox-e mono black" style="border-radius:50% 100%">50% 100%</section></td>
        </tr>
        <tr row="3">
            <td><section class="mbox-e mono black" style="border-radius:100% / 50%">100% / 50%
            </section></td>
            <td><section class="mbox-e mono black" style="border-radius:50% / 25%">50% / 25%; </section></td>
            <td><section class="mbox-e mono black" style="border-radius:50% / 100%">50% / 100%</section></td>
        </tr>
        <tr row="4">
            <td><section class="mbox-e mono black" style="border-radius:100% 0 0 0/ 50%">100% 0 0 0/ 50%
            </section></td>
            <td><section class="mbox-e mono black" style="border-radius:50% 0 0 0/ 50%">50% 0 0 0 / 50%; </section></td>
            <td><section class="mbox-e mono black" style="border-radius:100% 0 0 0 / 100%">100% 0 0 0 / 100%</section></td>
        </tr>
        <tr row="5">
            <td><section class="mbox-e mono black" style="border-radius:100% 0 0 100%/ 50%">100% 0 0 100% / 50%
            </section></td>
            <td><section class="mbox-e mono black" style="color:#009688;border-radius:50%/100% 100% 0 0">50% / 100% 100% 0 0</section></td>
            <td><section class="mbox-e mono black" style="border-radius:0 100% 100% 0 / 50%">0 100% 100% 0 / 50%</section></td>
        </tr>
        <tr row="6">
            <td><section class="mbox-e mono black" style="border-radius:100% 0 0 0">100% 0 0 0
            </section></td>
            <td><section class="mbox-e mono black" style="border-radius:999px 0 0 0">999px 0 0 0</section></td>
            <td><section class="mbox-e mono black" style="border-radius:80px 0 0 0">80px 0 0 0</section></td>
        </tr>
</tbody>
</table>
