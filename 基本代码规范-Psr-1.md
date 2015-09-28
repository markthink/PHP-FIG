[PHP Standard Recommendations](http://www.php-fig.org/psr/)
===

PSR-1
---
###Basic Coding Standard(基本代码规范)

本篇规范制定了代码基本元素的相关标准，以保证共享PHP代码之间技术互操作的编码要素。

关键词：MUST(必须)、MUST NOT(不能)、REQUIRED(需要)、SHALL(将会)、SHALL NOT(不会)、SHOULD(应该)、SHOULD NOT(不该)、RECOMMENDED(推荐)、MAY(可以)和OPTIONAL(可选)的详细描述可参考[RFC-2119](http://tools.ietf.org/html/rfc2119)

####概要
1. PHP代码文件必须以<?php或<?=标签开始
2. PHP代码文件必须以不带BOM的UTF-8编码
3. PHP代码中应该只定义类、函数、常量等声明，或其他会产生从属效应的操作(如生成文件输出以及修改.ini配置文件等),两者只能二选一
4. 命名空间以及类必须符合PSR的自动加载规范：PSR-0或PSR-4中的一个
5. 类的命名必须遵循大写开头的驼峰命名规范
6. 类中的常量所有字母必须大写，单词间用下划线分隔
7. 方法名称必须符合cameCase式的小写开头驼峰命名规范

####文件
PHP标签

php代码必须使用<?php ?>长标签或<?= ?>短标签输出，一定不可使用其它自定义标签

字符编码

PHP代码必须且只可使用不带BOM的utf-8编码

从属效应(Side Effects副作用)

一份PHP文件中应该要不就只定义新的声明，如类、函数或常量等不产生从属效应的操作，要不就只有会产生从属效应的逻辑操作，但不该同时包含两者。

从属效应一词的意思是指执行逻辑没有直接关系的声明类、函数或常量等，仅通过包含文件,不直接声明类。

从属效应包含却不仅限于生成输出，明确使用require或include连接外部服务、修改.ini配置、抛出错误或异常、修改全局或静态变量、读或写文件等。

下面是一个反例，一份同时包含声明以及产生从属效应的代码：

```php
<?php
//从属效应：修改ini配置
ini_set('error_reporting', E_ALL);

//从属效应：引入文件
include 'file.php';

//从属效应：生成输出
echo "<html>\n";

//声明函数
function foo()
{
	//函数主体部分
}
```
下面是一个范例，一份只包含声明不产生从属效应的代码：

```php
<?php
//声明函数
function foo()
{
	//函数主体部分
}
//条件声明 **不**属于从属效应
if(!function_exists('bar')){
	function bar()
	{
		//函数主体部分
	}
}
```
命名空间和类

命名空间以及类的命名必须遵循[PSR-0,PSR-4]

根据规范，每个类都独立为一个文件，且命名空间至少有一个层次：顶层的组织名称

类的命名必须遵循StudlyClass，大写开头的驼峰命名规范

PHP5.3及以后的版本代码必须使用正式的命名空间 例如：

```php
<php
//php5.3及以后版本的写法
namespace Vendor\Model;

class Foo
{
}
```
PHP5.2.x及以前的版本应该使用伪命名空间的写法，约定俗成使用顶级的组织名称如vendor_为类前缀

```php
<?php
//5.2.x及以前版本写法
class Vendor_Model_Foo
{
}
```
类的变量、属性和方法

此处的类指代表所有的类、接口以及可复用代码块(traits)

常量：

类常量所有字母必须大写声明，词间以下划线分隔 参照下列代码：

```php
<?php
namespace Vendor\Model;

class Foo
{
	const VERSION = '1.0';
	const DATE_APPROVED = '2015-10-01';
}
```
属性：

类的属性命名可以遵循 大写开头的驼峰式($StudlyClass)、小写开头的驼峰式($cameCase)又或是下划线分隔式($under_score)，本规范不做强制要求，但无论遵循哪种命名方式，都应该在一定范围内保持一致，这个范围可以是整个团队、整个包、整个类或是整个方法

方法：

方法名称必须符合caseCase()式的小写开头驼峰命名规范
