``Heredoc``技术，在正规的PHP文档中和技术书籍中一般没有详细讲述，只是提到了这是一种Perl风格的字符串输出技术。但是现在的一些论坛程序，和部分文章系统，都巧妙的使用heredoc技术，来部分的实现了界面与代码的准分离，phpwind模板就是一个典型的例子。

如下：

	<?php 
	$name = '浅水游';
	print <<<EOT
	
	<html> 
	<head> 
	<meta http-equiv="Content-Type" content="text/html; charset=gb2312" /> 
	<title>Untitled Document</title> 
	</head> 
	<body> 
	<!--12321--> 
	Hello,$name! 
	</body> 
	</html>
	
	EOT;
	?>

1.以<<<End开始标记开始，以End结束标记结束，结束标记必须顶头写，不能有缩进和空格，且在结束标记末尾要有分号 。开始标记和开始标记相同，比如常用大写的EOT、EOD、EOF来表示，但是不只限于那几个，只要保证开始标记和结束标记不在正文中出现即可。

2.位于开始标记和结束标记之间的变量可以被正常解析，但是函数则不可以。在heredoc中，变量不需要用连接符.或,来拼接，如下：
```	
	$v=2;
	$a= <<<EOF
	"abc"$v
	"123"
	EOF;
	echo $a; //结果连同双引号一起输出："abc"2 "123"
```

3.heredoc常用在输出包含大量HTML语法d文档的时候。比如：函数outputhtml()要输出HTML的主页。可以有两种写法。很明显第二种写法比较简单和易于阅读。
```
	function outputhtml(){
	echo "<html>";
	echo "<head><title>主页</title></head>"; 
	echo "<body>主页内容</body>";
	echo "</html>;
	}
	
	function outputhtml()
	{
	echo <<<EOT
	   <html>
	   <head><title>主页</title></head>
	   <body>主页内容</body>
	   </html>
	EOT;
	}
	
	outputhtml();
```