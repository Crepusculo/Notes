#

<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

      - [opacity - 比起说是"透明度", 应该说是"不透明度"](#opacity-比起说是透明度-应该说是不透明度)   
      - [opacity 默认继承](#opacity-默认继承)   
      - [在仅仅改变 background 的场合, 我们可以使用 rgba / hsla 来替代 tgb + opcaity 的方案。](#在仅仅改变-background-的场合-我们可以使用-rgba-hsla-来替代-tgb-opcaity-的方案。)   
      - [opacity 在子元素中重写并不是重新设置 而是叠加](#opacity-在子元素中重写并不是重新设置-而是叠加)   

<!-- /MDTOC -->

+ ### opacity - 比起说是"透明度", 应该说是"不透明度"
+ ### opacity 默认继承

<div class="green" style="opacity:0.8">
ww
<div class="red" style="opacity:0.8">ww
</div>
ww</div>

默认继承是无解的, 好在我们有多种可以尝试的替换方法

+ ### 在仅仅改变 background 的场合, 我们可以使用 rgba / hsla 来替代 tgb + opcaity 的方案。

old:
<div style="background:rgb(222,222,12); opacity:0.5">ww</div>
new:
<div style="background:rgba(222,222,12,0.5);">ww</div>
new2:
<div style="background:hsla(30,100%,50%,0.5);">ww</div>

+ ### opacity 在子元素中重写并不是重新设置 而是叠加

<div style="opacity:0.8">
opacity = 0.8
<div style="opacity:0.8">
opacity = 0.8*0.8 = 0.64
<div style="opacity:0.8">
opacity = 0.64*0.8 = 0.512
<div style="opacity:0.8">
ww
<div style="opacity:0.8">
ww
<div style="opacity:0.8">
ww
<div style="opacity:0.8">
ww
</div></div></div></div></div></div></div>

+ 使用 filter 为 opacity 回退
主要针对IE8 以下版本
(换句话说也就是没啥用)

filter:alpha(opacity=50);
<div style="filter:alpha(opacity=0);">
注意, 这个回退只在 IE8 以前的IE浏览器有效,
</div>
