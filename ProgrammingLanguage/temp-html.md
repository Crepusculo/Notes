> 主要用来上课写作关于 HTML/CSS/JS 的笔记

<style type="text/css">
        .green-line-title{
            background:#009C67;
            text-align:center;
            font-size: 1.5em;
        }
        .html{
            border:thin solid #009C67; padding:12px; margin:12px;
        }
</style>

<p class="green-line-title">所见即所得</p>

# 全局元素
## `accesskey`
+ 定义热键
+ Win 上为 Alt + [x]

<div class="html">
    <form>
    Name: <input type="text" name="name" accesskey="n"/>
    <br/>
    Password: <input type="text" name="password" accesskey="p"/>
    <br/>
    </form>
</div>

> 这个快捷键是游览器引擎在处理, 在 Atom 中被冲突的快捷键被拦截掉无法响应

## `class`
一个元素可以归于多个类别 其他略过不表

## `contenteditable` | HTML 5 new
用于允许用户修改页面上的内容

> typora 的即写即修改就是靠这个做的

<div class="html">
    <p contenteditable="true">It is editable right now</p>
</div>

+ [ ] 如何编写回调函数

## `contextmenu`
为元素编写快捷菜单

## `dir`
决定文字呈现方向 | 伟大的阿拉伯文????
<div class="html">
    <p dir="rtl">This is right-to-left</p>
    <p dir="ltr">This is left-to-right</p>
</div>

## `draggable` | `dropzone`
+ [ ] 拖动相关

## `hidden`
<div class="html">
<p>1. The Role Goals - Planning Manager</p>
<p id="hidden" hidden>2. The Role Goals - Planning Manager</p>
<p>3. The Role Goals - Planning Manager</p>
<p>4. The Role Goals - Planning Manager</p>
</div>

`hidden` 属性是 boolean 类型的
`hidden` 的元素不占位置

-----------


<div class="html">
</div>
<div class="html">
</div>
<div class="html">
</div>
