title: PHP7连接MySql错误 Uncaught Error: Call to undefined function mysql_connect()
date: 2016-06-20 17:02:58
tags:
---
## 搭建nginx + php + mysql 时 遇到了错误
首先来回顾一下环境搭建过程：
1.下载这三个玩意儿
2.启动nginx.exe,在浏览器中查看http://127.0.0.1, 看nginx是否工作正常
3.修改nginx.conf中的location来指向自己的index.html
  {% codeblock lang:html %}
  <html>
    <head></head>
    <body>hello</body>
  </html>
  {% endcodeblock%}
4.启动php, php-cgi.exe -b 127.0.0.1:9000
5.用netstat -a 来查看是否启动成功
6.php请求，修改nginx.conf文件中的location ~\.php 中的location,新建一个测试的php
  {% codeblock lang:php %}
  <?php>
    echo phpinfo();
  {% endcodeblock%}
7.php支持mysql，修改php.ini
  放开 extension_dir = "ext" 和 extension=php_mysql.dll
8.新建一个测试数据库的mysql_test.php
  {% codeblock lang:php %}
  <?php>
      $con = mysql_connect("localhost","root","");  
      if (!$con){  
      die('Could not connect: ' . mysql_error());  
      } else {  
      echo 'Database connected successfully';  
      }  
      mysql_close($con);
  {% endcodeblock%}
9.浏览器中输入http://127.0.0.1/mysql_test.php
  报错Fatal error: Uncaught Error: Call to undefined function mysql_connect()

##注意了~！敲黑板~！
##问题就出现在第7，8步

在下载的php文件夹里，php.ini文件里只有extension=php_mysqli.dll,并没有php_mysql.dll
当时居然天真的以为是教程里手误了~~~
然后就出现了后面的错误，卸载mysql又重装搞了半天

来分析一下错误：说是没有找到mysql_connect，原因是没有php_mysql.dll，但是怎么会没有这个dll呢？
因为人家就是已经不用这个了啊。

官网宝典 [php官网关于mysql的说明](http://php.net/manual/zh/mysqlinfo.api.choosing.php)

PHP7已经把”mysql.dll”删除，推荐使用mysqli或者PDO_MySQL
原文如下：

>It is recommended to use either the mysqli or PDO_MySQL extensions. It is not recommended to use the old mysql extension for new development, as it was deprecated in PHP 5.5.0 and was removed in PHP 7.

mysql,mysqli,PDO扩展所提供的API不同，连接数据库的API如下
``
// mysqli
$mysqli = new mysqli("example.com", "user", "password", "database");

// PDO
$pdo = new PDO('mysql:host=example.com;dbname=database', 'user', 'password');

// mysql
$c = mysql_connect("example.com", "user", "password");
``
mysql_connect是mysql.dll的API，改成mysqli,或者PDO方式访问。

##就是改成这样：

7.php支持mysql，修改php.ini
  放开 extension_dir = "ext" 和 extension=**php_mysqli.dll**
8.新建一个测试数据库的mysql_test.php
  {% codeblock lang:php %}
  <?php>
      $con = **new mysqli**("localhost","root","");  
      if (!$con){  
      die('Could not connect: ' . mysql_error());  
      } else {  
      echo 'Database connected successfully';  
      }  
      **mysqli_close**($con);
  {% endcodeblock%}
