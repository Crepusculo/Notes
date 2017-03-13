<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [引入 CSS](#引入-css)   
   - [使用元素内嵌样式](#使用元素内嵌样式)   
   - [使用文档内嵌样式](#使用文档内嵌样式)   
   - [使用外部样式表](#使用外部样式表)   
   - [从其它样式表导入样式](#从其它样式表导入样式)   
- [规定字符集](#规定字符集)   
- [层叠-继承-重要性](#层叠-继承-重要性)   
   - [浏览器样式 (用户代理样式)](#浏览器样式-用户代理样式)   
   - [用户样式](#用户样式)   
   - [__样式层叠顺序__](#__样式层叠顺序__)   
      - [用`!important`调整层叠次序](#用important调整层叠次序)   
   - [同级样式冲突](#同级样式冲突)   
   - [具体程度相同样式](#具体程度相同样式)   

<!-- /MDTOC -->
<style type="text/css" >
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

# 引入 CSS
## 使用元素内嵌样式

<div class="html">
<p style="color:#21ff99">使用 <code>style</code> 属性直接为标签指定 css 元素</p>
</div>

## 使用文档内嵌样式

```html
<html>
    <head>
        <title>Eg.</title>
        <style type="text/css">
            a {
                background: grey;
                color: white;
            }
            span {
                border: thin black solid;
                padding: 10px;
            }
        </style>
    </head>
    <body>
    </body>
</html>
```

## 使用外部样式表

文件 <span class="html">style.css</span>
```css
a {
    color: #212121;
}
span{
    color:inherit;
}
```
文件 <span class="html">index.html</span>
```html
<html>
    <head>
        <title>eg.2</title>
        <link rel="stylesheet" type="text/css" href="../css/style.css"/>
    </head>

```

> 选择器生效顺序: 生效的是后导入的样式

## 从其它样式表导入样式
文件 <span class="html">style2.css</span>

`@import "style.css"`

> `@import`使用并不广泛
> 浏览器对 `@import`语句的效率往往不如处理多个link元素并靠样式层叠解决问题

# 规定字符集
`@charset "UTF-8"`
如果没规定字符编码, 则浏览器将使用载入该样式表的 HTML 文档声明的编码
若 HTML 也没有声明, 则默认情况下使用 UTF-8

# 层叠-继承-重要性
除了 上面说到的三种定义样式表方式 ( 元素内嵌 文档内嵌 外部样式表 )还有另外两种:

__浏览器样式__ | __用户样式__

## 浏览器样式 (用户代理样式)
元素尚未设置样式时, 浏览器应用在它身上默认样式

## 用户样式
现代浏览器允许用户自定义样式表。
以 Chrome 为例, 在用户的个人配置路径下有一条
`Default\User StyleSheets\Custom.css` 可以自定义样式。


## __样式层叠顺序__
(1) 元素内嵌样式
(2) 文档内嵌样式
(3) 外部样式
(4) 用户样式
(5) 浏览器样式

前三种样式称为作者样式

### 用`!important`调整层叠次序

<div class="html">

<style type="text/css">
.green  {
    color:yellow !important; font-size: 1.8em
}
.green {
    color:green; font-size: 1em !important;
}
#important-test{
    color:red ; font-size: 10em;
}
</style>

<p id="important-test" class="green">あなたは日本語が<span>上手</span>です</p>
</div>

可以理解为

__作者定义的重要样式 > 用户定义的重要样式 > 作者样式 > 用户样式 > 浏览器样式__

## 同级样式冲突

> __较为特殊优先原则__
如果有两条定义于同一层次的样式都能应用同一个元素, 且它们都包含这浏览器要查看的CSS属性值, 这时需要冲突解决机制。

浏览器会评估两条样式的具体程度 然后选中较为特殊的那条。

样式的具体程度通过统计三类特征得出:

a. 样式的选择器中id值的数目
b. 选择其中其他属性和伪类的数目
c. 选择其中元素名和伪元素的数目

评分时按照 a-b-c 的形式, 生成一个数字, 只有两个元素的a相同的时候, 浏览器才会考虑 b 值
比如, 1-0-0 的得分比 0-5-5 这个得分代表的具体程度更高

## 具体程度相同样式
如果几条样式的具体程度相同, 
