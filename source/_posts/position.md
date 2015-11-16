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
可用于实现文字环绕图片

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
## inline_block
使用display属性的inline-block值可以实现浮动（不需要清除浮动）

1. vertical-align 属性会影响到inline-block元素，需要设置为top。
2. 需要设置每一列的宽度。
3. 如果HTML源代码中元素之间有空格，那么列于列之间会产生空隙。

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