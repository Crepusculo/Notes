<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [三层盒模型](#三层盒模型)
   - [box-shadow 多重边框](#box-shadow-多重边框)
   - [box-shadow + outline 双层边框](#box-shadow-outline-双层边框)
   - [border](#border)
- [background](#background)
   - [background](#background)
   - [background 多重背景详解](#background-多重背景详解)
   - [background 多重背景应用](#background-多重背景应用)
   - [background-blend-mode](#background-blend-mode)
- [盒模型的边和角的值简写语法](#盒模型的边和角的值简写语法)

<!-- /MDTOC -->

<style type="text/css">
.green{
    background:#009C67;
    text-align:center;
    font-size: 1.5em;
    color: white;
}
.red{
    background:#F4511E;
    text-align:left;
    padding-left: 16px;
    font-size: 1.2em;
    color: white
}
.html{
    border:thin solid #009C67; padding:12px; margin:12px;
}
.editable{
    background:#212121;
}
</style>

# 三层盒模型
`content-box` - `padding-box` - `border-box`

> CSS3 中支持多重边框
> 理论上盒模型可以扩展到n层
>
> <div class="html">
  <div style="width:300px; height:200px; margin:0 auto;
    box-shadow: 0 0 0 10px #655,
                0 0 0 15px teal;
    background: repeating-linear-gradient(45deg,
                #fb3, #fb3 15px, transparent 0,transparent 30px);
 ">两个外层 box-shadow叠加
 </div>
 </div>

>  <div class="html">
<div style="width:300px; height:200px; margin:0 auto;
  box-shadow: 0 0 0 10px #655 inset,
              0 0 0 15px teal ;
  background: repeating-linear-gradient(45deg,
              #fb3, #fb3 15px, transparent 0,transparent 30px);
">灰色往里扩展了
</div>
</div>

## box-shadow 多重边框

+ box-shadow 本来的作用是生存投影
+ 与 border 相比, box-shadow 最大的好处是可以生成任意数量的投影来模拟边框
+ box-shadow 层层叠加的方式是第一层位于层顶, 其后每一层位于下方
    + 其宽度是从边框算起的半径, 而不是从上一层 box-shadow 算起
+ 投影的行为和边框**不完全一致**
    + 投影不影响布局
    + 投影不受到 box-sizing 的影响
+ 用投影做出的虚假边框出现在元素的**外圈**,它们并不会响应鼠标事件。

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

+ `outline` 不接受多个值
+ `outline` 作用于padding-content盒模型外边, 但是不会贴合padding-content盒模型

## border

<div class="red">投影的内嵌和外扩(好像是给box-shadow属性加inset关键字)</div>

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


## background 多重背景应用

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
