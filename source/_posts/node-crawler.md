title: 用node来实现一个小爬虫~
date: 2015-12-03 14:40:10
tags:
---
### 用node来实现一个小爬虫~

首先require模块http，这里爬取的是北邮的主页

{% codeblock lang:javascript %}
var http = require('http');  
var url = 'http://www.bupt.edu.cn/';
{% endcodeblock%}

在开始的时候，先试着拿到整个页面的HTML:

{% codeblock lang:javascript %}
http.get(url, function(res) {
	var html = '';

	res.on('data', function(data) {
		html += data;
	});

	res.on('end', function() {
		console.log(html);
	});

}).on('error', function() {
	console.log('获取页面出错');
});
{% endcodeblock%}

是不是so easy~!

但是整个HTML代码并没有什么卵用，需要提取出中间有用的信息~！

这里需要用到一个模块 [cheerio](https://github.com/cheeriojs/cheerio) （语法类似于Jquery，主要用于爬虫）

同样 引入该模块

{% codeblock lang:javascript %}
var cheerio = require('cheerio');
{% endcodeblock%}

filterChapters方法用来提取主页中的章节（即顶部导航栏的内容）

{% codeblock lang:javascript %}
function filterChapters(html) {
	var $ = cheerio.load(html);
	var chapters = $('.top_nav');
	
	//数据结构
	// [{
	// 	chapterTitle: '',
	// 	sub: [
	// 		subTitle: '',
	// 		url: ''
	// 	]
	// }]
	
	var data = [];
	
	chapters.each(function(item) {
		var chapter = $(this);
		var chapterTitle = chapter.find('span').text();
		var subs = chapter.next().find('a');
	
		var chapterData = {
			chapterTitle: chapterTitle,
			sub: []
		}
		
		subs.each(function(item) {
			var sub = $(this);
			var subTitle = sub.text();
			var url = sub.attr('href');
	
			chapterData.sub.push({
				subTitle: subTitle,
				url: url 
			})
		});
	
		data.push(chapterData);
	});
	
	return data;

}
{% endcodeblock%}

打印的格式调整一下

{% codeblock lang:javascript %}
function printData(data) {
	data.forEach(function(item) {
		var chapterTitle = item.chapterTitle;
		console.log(chapterTitle + '\n');
	
		item.sub.forEach(function(sub) {
			console.log('  【' + sub.subTitle + '】  ' + sub.url + '\n');
		});
	})
}
{% endcodeblock%}

最终的样子就是这样：
{% img [crawler] /images/crawler.png %}

