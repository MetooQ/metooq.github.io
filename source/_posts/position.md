title: 各种CSS的布局酱~！
date: 2015-11-12 11:59:56
tags:
---

# 关于布局( *・ω・)✄╰ひ╯
---
## position

先来看看[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)上的好惹~

**初始值 static**
>元素正常表现，即元素处在文档流中它当前的布局位置，top\right\bottom\left\z-index属性无效


{% codeblock lang:css %}
position: static;
{% endcodeblock%}
默认值，设置为这个值则表示不会被特殊定位，一个static元素表示它不会被“positioned”

**定位元素 （非static）**
>定位元素是计算后位置属性为relative\absolute\fixed\sticky的元素，top\right\bottom\left\属性指定 **定位元素（即非static）** 的位置  

- 相对定位元素 (relative) 
{% codeblock lang:css %}
position: relative;
{% endcodeblock%}  
表现和static一样，除非添加一些额外的属性。  
设置top\right\bottom\left属性会使其偏离正常位置。其他元素并不会弥补它偏离以后剩下的空隙。

- 绝对定位元素（fixed和absolute）  
	- fixed  
	{% codeblock lang:css %}
	position: fixed;
	{% endcodeblock%}
	相对于视窗来定位，即便页面滚动，还会停留在相同的位置。（对移动端支持比较差，[这里](http://bradfrost.com/blog/mobile/fixed-position/)有解决方案）   
	- absolute（最棘手的家伙(ง •̀_•́)ง┻━┻）  
	{% codeblock lang:css %}
	position: absolute;
	{% endcodeblock%}  
	与fixed表现类似，是相对于最近的“positioned”父元素（offsetparent），所以它会随着页面滚动。

- sticky定位元素  
{% codeblock lang:css %}
position: -webkit-sticky; 
position:sticky; 
top: 15px;
{% endcodeblock%}
sticky是新的css3的属性，表现类似relative和fixed的合体，目标区域在屏幕可见时，是relative；超出目标区域时，为fixed，会固定在目标区域。


一共就这几个~！ლ(❛◡❛✿)ლ


---
## float
来自[EFE](http://efe.baidu.com/blog/float/)

**浮动元素的特点：**

- 浮动对于自身的影响：
> 1. 元素被视为块级元素，相当于display:block;
> 2. 元素具备包裹性，会根据它所包含的元素实现宽度和高度的自适应；


- 浮动对于兄弟元素的影响：
> 3. 浮动元素前后的块级兄弟元素会忽视浮动元素，并且占据它的位置，在浮动元素的下层，其他行内元素会环绕浮动元素；（**浮动元素最大的特点就是脱离了文档流,但是它依然占据着位置，这点是和绝对定位最大的不同**）
> 4. 浮动元素之前如果有浮动元素，如果方向相同，则会紧跟在后面，容器宽度不够时换行展示；
> 5. 浮动元素之间的水平间距不会折叠（**尽可能向边缘漂浮，但不越界**）；


- 浮动对于父元素的影响：
> 6. 容器内如果只有浮动元素，则容器会高度塌陷（**因为浮动元素的高度会被忽略**）；
> 7. 浮动元素的容器的非浮动兄弟，会忽视浮动元素，并覆盖浮动元素；
> 8. 浮动元素的容器的浮动兄弟，会跟随浮动元素，仿佛在一个容器内。

**(ゝ∀･)总结来说就是：块级元素重叠；行内元素环绕；浮动元素跟随。**

插播一条BFC的内容，具体[以后]()会写：

float对同一个BFC内的元素有效。如果父元素没有触发生成新的BFC，那么父元素的兄弟元素就都算是跟父元素中的元素处于同一BFC，也就会受浮动的影响，并且行为规则与同处于同一个父元素之中的元素的规则相同（上面的三条规则）。


### 实现并排的两种方法

#### float
**好处**
1. 天然的可以顶部上边框对齐，无需做位置微调  
2. 浮动元素之间没有空白间距

**坏处**
1. 浮动元素对元素背身，以及它的父元素，兄弟元素带来的影响非常大，使用浮动后要认真处理好浮动清除等事宜  
2. 当需要引用外部创建的空间，无法有效控制DOM结构和创建时机时，容易产生不可预知的bug

#### inline-block
**好处**   
简单、单纯、不会对其他元素造成影响ヽ( ^∀^)ﾉ  

**坏处**
1. 对齐问题，需要设置vertical-align为相同值，但在复杂结构中如果引入了外部控件，需要考虑。
2. 需要设置每一列的宽度。
3. 如果HTML源代码中元素之间有空格，那么列于列之间会产生空隙。

### 清除浮动
{% codeblock lang:css %}
 clear: left\right\both;
{% endcodeblock%}

 
 **but~!**

 使用浮动经常会遇到一个古怪的事情：图片比容器高时，就会溢出到容器外面  
 有一种丑陋的解决方案：  
{% codeblock lang:css %}
 overflow: auto;
{% endcodeblock%}

如果要支持IE6，需要加入  
{% codeblock lang:css %}
 overflow: auto;
 zoom: 1;
{% endcodeblock%}

还有一些“独特”的浏览器需要额外关照，[清除浮动这潭水好深的说](http://stackoverflow.com/questions/211383/which-method-of-clearfix-is-best)



---
## flex
### 使用flex来布局（来个厉害的）
{% codeblock lang:css %}
 .container {
  display: -webkit-flex;
  display: flex;
}
.initial {
  -webkit-flex: initial;
          flex: initial;
  width: 200px;
  min-width: 100px;
}
.none {
  -webkit-flex: none;
          flex: none;
  width: 200px;
}
.flex1 {
  -webkit-flex: 1;
          flex: 1;
}
.flex2 {
  -webkit-flex: 2;
          flex: 2;
}
{% endcodeblock%}

整个container大概长这样：  

initial | none | flex1 | flex2
------- | ---- | ----- | -----
空间足够时是200px,不够时是100px | 一直是200px | 占满剩余的1/3 | 占满剩余的2/3

### 使用flexbox的居中布局
{% codeblock lang:css %}
 .vertical-container {
  height: 300px;
  display: -webkit-flex;
  display:         flex;
  -webkit-align-items: center;
          align-items: center;
  -webkit-justify-content: center;
          justify-content: center;
}
{% endcodeblock%}

该容器内部的内容为垂直居中。

---
## 百分比宽度

对图片很有用 哦~  
简单的左右布局：    
{% codeblock lang:css %}
 nav {
   float: left;
   width: 25%;
 }
 section {
   margin-left: 25%
 }
{% endcodeblock%}

---
## 媒体查询

“响应式设计（Responsive Design）”是一种让网站针对不同的浏览器和设备“响应”不同显示效果的策略，这样可以让网站在任何情况下显示的很棒！

媒体查询是做此事所需的最强大的工具。让我们使用百分比宽度来布局，然后在浏览器变窄到无法容纳侧边栏中的菜单时，把布局显示成一列：

{% codeblock lang:css %}
@media screen and (min-width:600px) {
  nav {
    float: left;
    width: 25%;
  }
  section {
    margin-left: 25%;
  }
}
@media screen and (max-width:599px) {
  nav li {
    display: inline;
  }
}
{% endcodeblock%}

在[MDN](https://developer.mozilla.org/en-US/docs/CSS/Media_queries)上有媒体查询的具体内容  
**移动端** 使用 [meta viewport](http://dev.opera.com/articles/view/an-introduction-to-meta-viewport-and-viewport/)

---

## CSS布局的各种框架

[各种框架](http://zh.learnlayout.com/frameworks.html) 点这里~！（还有好多没有看(́◉◞౪◟◉‵)）