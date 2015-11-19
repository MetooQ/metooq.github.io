title: BFC(Block Formatting Contexts)
date: 2015-11-19 20:27:19
tags:
---
# BFC就是块级格式化上下文( ͡° ͜ʖ ͡°) 
---

### W3C中的定义
浮动元素、绝对定位元素、非块级盒子的块级元素（如inline-block, table-cells, table-captions)，以及overflow不为visible的块级盒子，都会为他们的内容创建新的BFC。  

     
在BFC中，盒子从顶端开始垂直地一个接一个排列，两个盒子之间的垂直间隙是由他们的margin值所决定的。在一个BFC中，两个相邻的块级盒子的垂直外边距会产生折叠。

### 可以这样理解

BFC是一个独立的布局环境，可以理解为一个箱子，箱子里边物品的摆放不受外界的影响。BFC的元素的布局不受外界的影响，因此往往利用这个特性来消除浮动元素对其非浮动的兄弟元素和其子元素带来的影响，在一个BFC中，块盒与行盒都会垂直的沿着其父元素的边框排列。


详细的内容可以看[这里](http://www.w3cplus.com/css/understanding-bfc-and-margin-collapse.html)

  
