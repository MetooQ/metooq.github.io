title: grunt学习笔记
date: 2015-11-27 14:14:07
tags:
---
## grunt学习笔记
---
### NodeJS

NodeJS可以用Javascript编写服务端程序


### Yeoman

WebApp的脚手架工具。在立项阶段，用于生成项目的文件和代码结构。代码校验、测试、压缩

``
npm install -g yo
``

### Bower

> 澳洲的一种鸟，雄鸟在求偶的时候会用树枝来搭建凉亭，并用色彩鲜艳的物品来装饰，吸引雌鸟


依赖包的管理工具，跟踪管理框、库、公共部分等

``
npm install -g bower
``

### Grunt

自动化：压缩、编译、单元测试、代码校验

``
npm install -g grunt-cli
``

---
### Yeoman实践

**生成器generator**

angular

``
yo angular name
``


### Bower实践

**包管理器**

将jquery 放到项目中
``
bower install jquery
``

在项目中会多一个bower_components文件夹，里边会有jquery的源码


也可以直接用github短语来安装(注册账号/项目名)
``
bower install jquery/jquery
``
还可以使用完整的github地址来安装
``
bower install url
``




