
[PHP Standard Recommendations](http://www.php-fig.org/psr/)
===

PSR-2
---
###Coding Style Guide（编码风格规范）


本规范是PSR-1的继承与扩展

本规范希望通过制定一系列规范化PHP代码的规则，以减少在浏览不同作者的代码时，因代码风格的不同而造成的不便。

当多名程序员在多个项目中合作时，就需要一个共同的编码规范，而本文中的风格规范源于多个不同项目代码风格的共同特性，因此，本规范的价值在于我们都遵循这个编码风格，而不是在于它的本身。

关键词：MUST(必须)、MUST NOT(不能)、REQUIRED(需要)、SHALL(将会)、SHALL NOT(不会)、SHOULD(应该)、SHOULD NOT(不该)、RECOMMENDED(推荐)、MAY(可以)和OPTIONAL(可选)的详细描述可参考[RFC-2119](http://tools.ietf.org/html/rfc2119)

####概览
1. 代码必须遵循PSR-1中的编码规范
2. 代码必须使用4个空格缩进，而不是TAB键进行缩进
3. 每行的字符数应该软限制在80个之内，理论上一定不可多于120个，但一定不能有硬性限制
4. 每个namespace命名空间声明语句和use声明语句块后面，必须插入一个空白行
5. 类的开始花括号({)必须写在函数声明后自成一行，结束花括号(})也必须写在函类主体后自成一行
6. 方法的开始花括号({)必须写在函数声明后自成一行，结束花括号(})也必须写在函数主体后自成一行
7. 类的属性和方法必须添加访问修饰符(private、protected以及public),abstract以及final必须声明在访问修饰符之前，而static必须声明在访问修饰符之后
8. 控制结构的关键字后必须要有一个空格符，而调用方法或函数时则一定不能有
9. 控制结构的开始花括号({)必须写在声明的同一行，而结束花括号(})必须写在主体后自成一行
10. 控制结构的开始左括号后和结束右括号前，都一定不能有空格符

例子：
以下例子程序简单地展示了以上大部分规范

	<?php
	namespace Vendor\Package;
	
	use fooInterface;
	use BarClass as Bar;
	use OtherVendor\OtherPackage\BazClass;
	
	class Foo extends Bar implements FooInterface
	{
		public function sampleFunction($a,$b=null)
		{
			if ($a === $b){
				bar();
			} elseif ($a > $b) {
				$foo->bar($arg1);
			} else {
				BazClass::bar($arg2, $arg3);
			}
		}
		
		final public static function bar()
		{
			//method body
		}
	}
	
通则：

基本编码规范

代码必须遵循PSR-1中的所有规范

文件：

所有PHP文件必须使用Unix LF(linefeed)作为行的结束符

所有PHP文件必须以一个空白行作为结束

纯PHP代码文件必须省略最后的?>结束标签

行：

行的长度一定不能有硬性的约束

软性的长度约束一定要限制在120个字符内，若超过此长度，带代码规范检查的编辑器一定要发出警告，不过一定不可发出错误提示

每行不应该多于80个字符，大于80字符的行应该折成多行

非空行后一定不能有多余的空格符

空行可以使得阅读代码更法方便以及有助于代码的分块

每行一定不能存在多于一条语句

缩进：

代码必须使用4个空格的缩进，一定不能用TAB键

备注：使用空格而不是tab键的好处在于，避免在比较代码差异、打补丁、重阅代码以及注释时产生混淆，并且，使用空格缩进，让对齐变得更加方便。

关键字以及TRUE/FALSE/NULL

PHP所有关键字必须全部小写

常量true、false和null也必须全部小写

namespace以及use声明

namespace声明后必须插入一个空白行

所有use必须在namespace后声明 

每条use声明语句必须只有一个use关键词

use声明语句块后必须要有一个空白行

例如
	<?php
	namespace Vendor\Package;
	
	use FooClass;
	use BarClass as Bar;
	use OtherVendor\OtherPackage\BazClass;
	
	//additional PHP code..

类、属性和方法

此处的类泛指所有的Class类、接口以及traits可复用代码块

扩展与继承

关键词 extends和implements必须写在类名称的同一行

类的开始花括号必须独占一行，结束花括号也必须在类主体后独占一行

例：
	<?php
	namespace Vendor\Package;
	
	use FooClass;
	use BarClass as Bar;
	use OtherVendor\OtherPackage\BazClass;
	
	class ClassName extends ParentClass implements \ArrayAccess, \Countable
	{
		//constans,properties,methods
	}

implements的继承列表也可以分成多行，这样的话，每个继承接口名称都必须分开独立成行，包括第一个
	<?php
	namespace Vendor\Package;
	
	use FooClass;
	use BarClass as Bar;
	use OtherVendor\OtherPackage\BazClass;
	
	class ClassName extends ParentClass implements 
		\ArrayAccess, 
		\Countable,
		\Serializable
	{
		//constans,properties,methods
	}

属性：

每个属性都必须添加访问修饰符

一定不可使用关键字var声明一个属性

每条语句一定不可定义超过一个属性

不要使用下划线作为前缀，来区分属性是protected或private.

下面是一个属性声明范例：
	<?php
	namespace Vendor\Package;
	
	class ClassName
	{
		public $foo = null;
	}	

方法：

所有方法都必须添加访问修饰符

不要使用下划线作为前缀，来区分方法是protected或private

方法名称后一定不能有空格符，其开始花括号必须独占一行，结构花括号也必须在方法主体后单独成一行，参数左括号和右括号前一定不能有空格。

一个标准的方法声明可以参照以下范例，留意其括号、逗号、空格以及花括号的位置
	
	<?php
	namespace Vendor\Package;
	
	class ClassName
	{
		public function fooBarBaz($arg1, &$arg2, $arg3=[])
		{
			//method body
		}
	}
方法的参数

参数列表中，每个参数后面必须要有一个空格，而前面一定不能有空格

有默认值的参数，必须放到参数列表的末尾

	<?php
	namespace Vendor\Package;
	
	class ClassName
	{
		public function foo($arg1, &$arg2, $arg3 = [])
		{
			//method body
		}
	}
参数列表可以分列成多行，这样，包括第一个参数在内的每个参数都必须单独成行

拆分成多行的参数列表后，结束括号以及方法开始括号必须写在同一行，中间用一个空格分隔

	
	<?php
	namespace Vendor\Package;
	
	class ClassName
	{
		public function foo(
			$arg1, 
			&$arg2, 
			$arg3 = []
		) {
			//method body
		}
	}

abstract、final以及static

需要添加abstract或final声明时，必须写在访问修饰符前，而static则必须写在其后

	<?php
	namespace Vendor\Package;
	
	abstract class ClassName
	{
		protected static $foo;
		
		abstract protected function zim();
		
		final public static function bar()
		{
			//method body
		}
	}
方法及函数调用

方法及函数调用时，方法名或函数名与参数左括号之间一定不能有空格，参数右括号前也一定不能有空格，每个参数前一定不能有空格，但其后必须有一个空格。

	<?php
	bar();
	$foo->bar($arg1);
	Foo::bar($arg2, $arg3);

参数可以分列成多行，此时包括每个参数在内的每个参数都必须单独成行

	<?php
	$foo->bar(
		$longArgument,
		$longerArgument,
		$muchLongerArgument
	);
	
控制结构：

控制结构的基本规范如下：

1. 控制结构关键词后必须有一个空格
2. 左括号(后一定不能有空格
3. 右括号)前也一定不能有空格
4. 右括号)与开始花括号{之间一定有一个空格
5. 结构体主体一定要有一次缩进
6. 结束花括号}一定在结构体主体后单独成行

if 、 elseif 和 else

标准的 if 结构如下代码所示，留意 括号、空格以及花括号的位置，

注意 else 和 elseif 都与前面的结束花括号在同一行。

	<?php
	if ($expr1) {
    	// if body
	} elseif ($expr2) {
    	// elseif body
	} else {
    	// else body;
	}
应该使用关键词 elseif 代替所有 else if ，以使得所有的控制关键字都像是单独的一个词。

switch 和 case

标准的 switch 结构如下代码所示，留意括号、空格以及花括号的位置。

case 语句必须相对 switch 进行一次缩进，而 break 语句以及 case 内的其它语句都 必须 相对 case 进行一次缩进。

如果存在非空的 case 直穿语句，主体里必须有类似 // no break 的注释。

	<?php
	switch ($expr) {
    	case 0:
        	echo 'First case, with a break';
        	break;
    	case 1:
        	echo 'Second case, which falls through';
        	// no break
    	case 2:
    	case 3:
    	case 4:
        	echo 'Third case, return instead of break';
        	return;
    	default:
        	echo 'Default case';
        	break;
	}

while 和 do while

一个规范的 while 语句应该如下所示，注意其 括号、空格以及花括号的位置。

	<?php
	while ($expr) {
    	// structure body
	}
	
标准的 do while 语句如下所示，同样的，注意其 括号、空格以及花括号的位置。

	<?php
	do {
   	 	// structure body;
	} while ($expr);
	
for

标准的 for 语句如下所示，注意其 括号、空格以及花括号的位置。

	<?php
	for ($i = 0; $i < 10; $i++) {
    	// for body
	}
	foreach

标准的 foreach 语句如下所示，注意其 括号、空格以及花括号的位置。

	<?php
	foreach ($iterable as $key => $value) {
    	// foreach body
	}

try, catch

标准的 try catch 语句如下所示，注意其 括号、空格以及花括号的位置。

	<?php
	try {
    	// try body
	} catch (FirstExceptionType $e) {
    	// catch body
	} catch (OtherExceptionType $e) {
    	// catch body
	}

闭包

闭包声明时，关键词 function 后以及关键词 use 的前后都必须要有一个空格。

开始花括号必须写在声明的同一行，结束花括号必须紧跟主体结束的下一行。

参数列表和变量列表的左括号后以及右括号前，必须不能有空格。

参数和变量列表中，逗号前必须不能有空格，而逗号后必须要有空格。

闭包中有默认值的参数必须放到列表的后面。

标准的闭包声明语句如下所示，注意其 括号、逗号、空格以及花括号的位置。

	<?php
	$closureWithArgs = function ($arg1, $arg2) {
    	// body
	};

	$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    	// body
	};
	
参数列表以及变量列表可以分成多行，这样，包括第一个在内的每个参数或变量都必须单独成行，而列表的右括号与闭包的开始花括号必须放在同一行。

以下几个例子，包含了参数和变量列表被分成多行的多情况。

	<?php
	$longArgs_noVars = function (
    	$longArgument,
    	$longerArgument,
    	$muchLongerArgument
	) {
  	 	// body
	};

	$noArgs_longVars = function () use (
    	$longVar1,
    	$longerVar2,
    	$muchLongerVar3
	) {
	   // body
	};

	$longArgs_longVars = function (
   		$longArgument,
    	$longerArgument,
    	$muchLongerArgument
	) use (
    	$longVar1,
    	$longerVar2,
    	$muchLongerVar3
	) {
	   // body
	};

	$longArgs_shortVars = function (
    	$longArgument,
    	$longerArgument,
    	$muchLongerArgument
	) use ($var1) {
   		// body
	};

	$shortArgs_longVars = function ($arg) use (
    	$longVar1,
    	$longerVar2,
    	$muchLongerVar3
	) {
   		// body
	};
	
注意，闭包被直接用作函数或方法调用的参数时，以上规则仍然适用。

	<?php
	$foo->bar(
    	$arg1,
    	function ($arg2) use ($var1) {
        	// body
    	},
    	$arg3
	);

总结

以上规范难免有疏忽，其中包括但不仅限于：

全局变量和常量的定义

函数的定义

操作符和赋值

行内对齐

注释和文档描述块

类名的前缀及后缀

最佳实践