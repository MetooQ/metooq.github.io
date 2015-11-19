title: margin折叠起来
date: 2015-11-19 10:00:28
tags:
---
# margin折叠起来~
---

在CSS1中对于margin折叠的说明：
> 原文：The width of the margin on non-floating block-level elements specifies the minimum distance to the edges of surrounding boxes. Two or more adjoining vertical margins (i.e., with no border, padding or content between them) are collapsed to use the maximum of the margin values. In most cases, after collapsing the vertical margins the result is visually more pleasing and closer to what the designer expects.  

> 翻译：外边距用来指定非浮动元素与其周围盒子边缘的最小距离。两个或两个以上的相邻的垂直外边距会被折叠并使用它们之间最大的那个外边距值。多数情况下，折叠垂直外边距可以在视觉上显得更美观，也更贴近设计师的预期。

总结来说就是：  
1. 发生折叠需要时**相邻**的非浮动元素；  
2. 折叠发生在垂直外边距上，即margin-top\margin-bottom；  
3. 折叠后取其中最大的margin值作为最终值；  

ps:**相邻**指的是处于同一个块级上下文中的块元素，没有行框，没有间隙，没有内边距和边框隔开它们。


### 如何避免margin折叠

**margin折叠的条件**

1. margin折叠元素只发生在块元素上；
2. 浮动元素不与其他元素margin折叠；
3. 创建了新的块级格式化上下文（BFC）的块元素，不与它的子元素发生margin折叠；
4. 绝对定位元素的margin不与其他任何margin发生折叠

因此避免的方法有很多，改成把它非块级，让它浮动，让它绝对定位，让它overflow:hidden，用边框隔开它们……等等等……

具体参考[这里](http://www.ituring.com.cn/article/64583)

