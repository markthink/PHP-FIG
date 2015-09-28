
[PHP Standard Recommendations](http://www.php-fig.org/psr/)
===

PSR-4
---
###Improved Autoloading(代码自动载入改进版本规范)

自动加载改进版本 - 也是目前推荐的版本 

PSR-4规范比较干净，去除了兼容PHP5.3以前版本的内容，此规范是PSR-0的必要补充，也可替代PSR-0.

最大的区别是对下划线的定义不同，PSR-4中，在类名中使用下划线没有任何特殊含义，而PSR-0则规定类名中的下划线会转化成目录分隔符。

关键词：MUST(必须)、MUST NOT(不能)、REQUIRED(需要)、SHALL(将会)、SHALL NOT(不会)、SHOULD(应该)、SHOULD NOT(不该)、RECOMMENDED(推荐)、MAY(可以)和OPTIONAL(可选)的详细描述可参考[RFC-2119](http://tools.ietf.org/html/rfc2119)

####概要
本PSR是关于由文件路径自动载入对应类的相关规范，它是完全互操作的，可以作为任一自动载入规范的补充，其中包括PSR-0。此外本PSR还包括自动载入的类对应的文件存放路径规范。

####规范要求
1. 术语类泛指所有的class类、interfaces接口、traits可复用代码以及其他类似结构
2. 一个完全限定类名具有如下形式:

	`\命名空间\(子命名空间)\*<类名>·\`
	
	1. 完全限定类名必须要有一个顶级命名空间，被称为供应商命名空间
	2. 完全限定类名可以有一个名多个子命名空间
	3. 完全限定类名必须有一个最终的类名
	4. 完全限定类名中任意一部分中的下划线都是没有特殊含义的
	5. 完全限定类名可以由任意大小写字母组成
	6. 所有类名都必须是大小写敏感的
3. 根据完全限定类名载入相应的文件
	1. 完全限定类名中，去掉最前面的命名空间分隔符，前面连续的一个或多个命名空间和子命名空间，作为命名空间前缀，其必须与至少一个文件基目录相对应。
	2. 紧接命名空间前缀后的子命名空间必须与相应的文件基目录相匹配，其中的命名空间分隔符将作为目录分隔符
	3. 末尾的类名必须与对应的以.php为后缀的文件同名
	4. 自动加载器的实现一定不能抛出异常，一定不能触发任一级别的错误信息以及不应该有返回值
	
例子：

| 完全限定类名  | 命名空间前缀  | 文件基目录 |  文件路径 |
| ------------ |---------------| -----| ----- |
|\Acme\Log\Writer\File_Writer|Acme\Log\Writer|./acme-log-writer/lib/|./acme-log-writer/lib/File_Writer.php|
|\Aura\Web\Response\Status|Aura\Web|/path/to/aura-web/src/|/path/to/aura-web/src/Response/Status.php|
|\Symfony\Core\Request|Symfony\Core|./vendor/Symfony/Core/|./vendor/Symfony/Core/Request.php|
|\Zend\Acl|Zend|/usr/includes/Zend/|/usr/includes/Zend/Acl.php|

	
###PSR-0和PSR-4异同：

1. 在composer.json定义ns，psr-4必须以\结尾否则会抛出异常，psr-0则不要求
2. psr-0类含下划线变转换成路径分隔符，psr-4则不存在实际意义
3. psr-0有更深的目录结构，比如定义ns为：

	Foo\Bar => vendor\foo\bar\src,
	
	调用：use Foo\Bar\Tool\Reuqest
	psr-0加载的实际路径是 vendor\foo\bar\src\Foo\Bar\Tool\Request.php
	psr-4加载的实际路径是 vendor\foo\bar\src\Tool\Request.php
	
PSR-4优点：

`较浅的目录结构、更灵活的文件位置、停止在类名使用下划线分隔、更明确的互操作性`

