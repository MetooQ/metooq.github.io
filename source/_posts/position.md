title: position
date: 2015-11-12 11:59:56
tags:
---

# positon的取值

先来看看[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)上的好惹~

**初始值 static**
>元素正常表现，即元素处在文档流中它当前的布局位置，top\right\bottom\left\z-index属性无效

**定位元素 positioned**
>定位元素是计算后位置属性为relative,absolute,fixed或sticky的元素
>相对定位元素 relatively
{% codeblock lang:css %}
position:relative;
{% endcodeblock%}
>绝对定位元素 absolutely
{% codeblock lang:css %}
position:absolute;
position:fixed;
{% endcodeblock%}
>sticky定位元素
{% codeblock lang:css %}
position:sticky;
{% endcodeblock%}

>top right bottom left 属性指定 **定位元素（即非static）** 元素的位置
