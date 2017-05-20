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
