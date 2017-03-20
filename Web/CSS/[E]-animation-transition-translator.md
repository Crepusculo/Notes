<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [Introduction](#introduction)   
   - [transition-property](#transition-property)   
   - [transition-duration](#transition-duration)   
   - [transition-timing-function](#transition-timing-function)   
   - [transition-delay](#transition-delay)   
   - [animation-name](#animation-name)   
   - [animation-duration | animation-timing-funtion](#animation-duration-animation-timing-funtion)   
   - [animation-delay](#animation-delay)   
   - [animation-iteration-count](#animation-iteration-count)   
   - [aniamtion-direction](#aniamtion-direction)   
   - [不在 animation 中简写的 animation 属性](#不在-animation-中简写的-animation-属性)   
      - [aniamtion-play-state](#aniamtion-play-state)   
      - [aniamtion-fill-mode](#aniamtion-fill-mode)   
   - [trans](#trans)   
- [Animation & Transition](#animation-transition)   

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
.consolas{
    font-family: consolas;
}
</style>

# Introduction

<div class="html">
<p class="green consolas">transition</p>

兼容性:
http://www.css88.com/book/css/properties/transition/transition.htm#compatible
(目前主流浏览器全部支持)

+ translation-property : 规定设置过渡效果的目标 CSS 属性名称
+ translation-duration : 规定过渡效果的时间
+ translation-timing-function : 规定速度效果的速度取现
+ transition-delay : 定义过渡效果开始的延迟

语法

```
transition: property duration timing-function delay;
```

| | |
|---|---|
| **默认值**  |  all 0 ease 0 |
| **继承性**  |  no |
| **版本**    | CSS3 |

> transition 的拆分写法:
> 由于需要一一对应所以其实不是很方便
> ```
> transition-property: border-color, background-color, color;
> transition-duration: .5s, .5s, .5s;
> transition-timing-function: ease-in, ease-in, ease-in;
> transition-delay: .1s, .1s, .1s;
> ```

---

## transition-property
默认值: none;
继承性: no;
```
transition-property: none|all|property;
```

---

## transition-duration
默认值: 0;
继承性: no;
规定完成过渡效果需要花费的时间（以秒或毫秒计）。
默认值是 0，意味着不会有效果。

```
transition-duration: time;
```
> 使用`transition`时务必注意必须设置 `transition-duration`, 否则默认时间为 0, 无效果

---

## transition-timing-function
```
transition-timing-function: linear|ease|ease-in|ease-out|ease-in-out|cubic-bezier(n,n,n,n);
```

解释:
| 值 |  描述 |
|---|---|
| <p class="consolas">linear</p>  | 以相同速度开始至结束的过渡效果<br/>等于 cubic-bezier(0,0,1,1)   |
| <p class="consolas">ease</p>  | 慢速开始，然后变快，然后慢速结束的过渡效果<br/>cubic-bezier(0.25,0.1,0.25,1)  |
| <p class="consolas">ease-in</p>  | 规定以慢速开始的过渡效果<br/>等于 cubic-bezier(0.42,0,1,1)  |
| <p class="consolas">ease-out</p>  | 规定以慢速结束的过渡效果<br/>等于 cubic-bezier(0,0,0.58,1)。  |
| <p class="consolas">ease-in-out</p>  | 规定以慢速开始和结束的过渡效果<br/>等于 cubic-bezier(0.42,0,0.58,1)。  |
| <p class="consolas">cubic-bezier(n,n,n,n)</p> | 在 cubic-bezier 函数中定义自己的值。n可能的值是 0 至 1 之间的数值。    |

w3school体验装:
http://www.w3school.com.cn/tiy/t.asp?f=css3_transition-timing-function2
http://www.w3school.com.cn/tiy/t.asp?f=css3_transition-timing-function3
使用 cubic-bezier 构建网站:
http://cubic-bezier.com/
---

## transition-delay
默认值：0
继承性：no
transition-delay 属性规定过渡效果何时开始
transition-delay 值以秒或毫秒计
```
transition-delay: time;
```
</div>



<div class="html">
<p class="green consolas">animation</p>

```
animation: name duration timing-function delay iteration-count  direction;
```
Safari 和 Chrome 支持替代的 -webkit-animation- 属性。
IE9以及更早版本不支持 animation 族的属性。

|   |   |
|---|---|
| animation-name  | 绑定的 keyframe 的名字  |
| animation-duration  | animation 演出持续时间 |
| animation-timing-function  | 时间函数 |
| animation-delay  | 延迟开始 |
| animation-iteration-count | 重复次数 |
| animation-name-direction  | 是否应该轮流反向播放动画 |

animation的非简写属性:

## animation-name
为 @keyframes 动画规定一个名称, 取的名字会绑定到选择器的 keyframe 名称上。

## animation-duration | animation-timing-funtion
和`transition`属性的一样, 在此略过

## animation-delay
Safari 和 Chrome 支持替代的 -webkit-animation- 属性。

animation 的 delay 值可以为负数, 表示"跳过n单位的动画周期"

比如 `-2s` 使动画马上开始，但跳过 2 秒进入动画。

> 在 `animation-iteration-count` 设置 n(n>1)或infinite 时, 只有第一次动画使负数生效, 跳过秒数, 剩下的动画依然会从 0 开始播放。

## animation-iteration-count
Safari 和 Chrome 支持替代的 -webkit-animation- 属性。

```
animation-iteration-count: n|infinite;
```
动画重复次数

> 只会影响 animation-delay属性 第一次的时间轴, 这也就是上面的注解中的情况出现的原因

## aniamtion-direction
Safari 和 Chrome 支持替代的 -webkit-animation- 属性。

默认值: normal
继承性: no

animation-direction 属性定义是否应该轮流反向播放动画。
```
animation-direction: normal|alternate;
```
如果 animation-direction 值是 "alternate"，则动画会在奇数次数（1、3、5 等等）正常播放，而在偶数次数（2、4、6 等等）向后播放。

## 不在 animation 中简写的 animation 属性

### aniamtion-play-state
Safari 和 Chrome 支持替代的 -webkit-animation- 属性。

规定动画是否正在运行或暂停。
默认值: `running`
继承性:
```
animation-play-state: paused|running;
```

### aniamtion-fill-mode
规定对象动画时间之外的状态。
Safari 和 Chrome 支持替代的 -webkit-animation-fill-mode 属性。


</div>

<div class="html">
<p class="green consolas">transfromer</p>

## trans
</div>

# Animation & Transition
首先明确一点, 简单认为 `animation` 是 `transition` 的替代是错误的,

`transition`是从**一个状态**平滑地过渡到**另一个状态**
`animation` 是从任意数量关键帧(keyframe)之间相互转化
