[PHP Standard Recommendations](http://www.php-fig.org/psr/)
===

PSR-0
---
###Autoloading Standard(代码自动载入规范)

`不推荐使用 - 2014年10月21日PSR-0已被标记为过时。 PSR-4，现在推荐作为替代。`

####规范要求：

1. 一个完全合格的命名空间和类名必须有以下结构"\提供者名称\(命名空间\)*<类名>"
2. 每个命名空间必须有顶层的命名空间(“供应商名称”)
3. 每个命名空间可以有任意多个子命名空间
4. 从文件系统加载时每个命名空间分隔被转换为"操作系统路径分隔符(DIRECTORY_SEPARATOR)"
5. 在类名的每个"_"字符转换为DIRECTORY_SEPARATOR. 该_字符在命名空间中没有任何特殊含义
6. 完全限定的命名空间和类从文件系统加载以".php"结尾的文件
7. 提供商名称、命名空间、类名可以由大小写字母组成，其中命名空间和类名是大小写敏感的以保证多系统兼容性

例子：

```php
\Doctrine\Common\IsolatedClassLoader => /path/to/project/lib/vendor/Doctrine/Common\IsolatedClassLoader.php
```
有下划线例子：

```php
\namespace\package\Class_Name => /path/to/project/lib/vender/namespace/package/Class/Name.php
```
载入样例：

```php
<?php
	function autoload($className)
	{
		$className = ltrim($className, '\\');
		$fileName  = '';
		$namespace = '';
		if ($lastNsPos = strrpos($className, '\\')) {
    		$namespace = substr($className, 0, $lastNsPos);
    		$className = substr($className, $lastNsPos + 1);
    		$fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
		}
		$fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

		require $fileName;
	}
	spl_autoload_register('autoload');
```
