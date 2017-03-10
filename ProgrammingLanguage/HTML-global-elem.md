


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
</style>

<p class="green">所见即所得</p>

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

<div class="red"> 如何编写回调函数 </div>

## `contextmenu`
为元素编写快捷菜单

## `dir`
决定文字呈现方向 | 伟大的阿拉伯文????
<div class="html">
    <p dir="rtl">This is right-to-left</p>
    <p dir="ltr">This is left-to-right</p>
</div>

## `draggable` | `dropzone`
<div class="red">拖动相关</div>


## `hidden`
<div class="html">
<p>1. The Role Goals - Planning Manager</p>
<p id="hidden" hidden>2. The Role Goals - Planning Manager</p>
<p>3. The Role Goals - Planning Manager</p>
<p>4. The Role Goals - Planning Manager</p>
</div>

`hidden` 属性是 boolean 类型的
`hidden` 的元素不占位置

<div class="red"><code>hidden</code> / <code>display:none</code> ?</div>

## `id`
标识与导航

## `lang`
<div class="html">
<p lang="en">Hello - how are you?</p>
<p lang="zh">Nihao</p>
</div>

让浏览器调整其表达元素内容的方式。
比如
+ 改变使用的引号,
+ 文字朗读器正确发音,

<div class="red"> 全局lang ?</div>

## `spellcheck`
仅在可编辑元素上使用有意义

<div class="html">
<textarea spellcheck="true" style="width:300px;">
This is some mispelled text
</textarea>
</div>

<div class="red"> Not work </div>

## `style`
CSS指定样式
在CSS中详解

## `tabindex`
Tab 选中顺序
标记为 "-1" 的值不会被选中
<div class="html">
<button tabindex="100" style="background:teal;  color:white;">first button</button>
<button tabindex="-1" style="background:teal;  color:white;">first button</button>
<button tabindex="99" style="background:teal;  color:white;">first button</button>
</div>

> 可以在浏览器中打开测试 但是在atom里不好用

## `title`
为元素提供额外元素 浏览器通常用这些东西显示工具提示。
<div class="html">
<a title="Float Hint" href="https://www.google.jp.cn">Float herf test</a>
</div>




-----------


<div class="html"></div>
<div class="red"></div>
<div class="green"></div>
