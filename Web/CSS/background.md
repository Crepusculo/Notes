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
>   <div style="width:300px; height:200px; margin:0 auto;
>   background-cilp: content-box;
>   background-image:    url(assets\4.gif), url(assets\4.gif), url(assets\4.gif);
>   background-position: left top,  50% 30%,   10px 100px;
>   background-size:     50px 50px, 50px 50px, 50px, 50px 50px;
>   box-shadow: 0 0 0 10px #655,
>               0 0 0 15px teal,
>               0 2px 5px 15px rgba(0,0,0,.6)"
> ">
> </div>
> </div>

<div class="red">多重背景没起作用 多重边框倒是work了</div>

## box-shadow 多重边框

+ box-shadow 本来的作用是生存投影
+ 与 border 相比, box-shadow 最大的好处是可以生成任意数量的投影来模拟边框
+ box-shadow 层层叠加的方式是第一层位于层顶, 其后每一层位于下方
    + 其宽度是从边框算起的半径, 而不是从上一层 box-shadow 算起
+ 投影的行为和边框**不完全一致**
    + 投影不影响布局
    + 投影不受到 box-sizing 的影响
+ 用投影做出的虚假边框出现在元素的**外圈**,它们并不会响应鼠标事件。

<div class="red">投影的内嵌和外扩(好像是给box-shadow属性加inset关键字)</div>

## background 多重背景详解
