# PHP注释规范
注释在写代码的过程中非常重要，好的注释能让你的代码读起来更轻松，在写代码的时候一定要注意注释的规范。  
“`php`是一门及其容易入门的语言，刚入门的新手不到几分钟的时间可能就会用`echo`打印出一个`hello world`！但是他是真正的程序员吗？怎么来定义程序员呢？如果想真正成为一个程序员，那么就必须遵循一套程序书写规范，”  
我们经常编写一些函数，但是这些函数可能也只有自己能看得懂，甚至过一段时间自己也不认识自己写的了，那么怎么办呢？最好的办法当然是给给自己的代码加上注释。  
我们可能熟悉很多注释的写法`C pear PHP`注释等等，但我们用到的主要还是`# `和`/**/`。
`#`是一种简短的注释方法。可能你会用它去注释一个变量，或者调用的一个方法。`/**/`我们可能还在用它去注释掉一大段代码，但是怎么用它去标准的注释一个函数呢？  

```php
/**
* @name 名字
* @abstract 申明变量/类/方法
** @access <private|protected|public>
* @author 函数作者的名字和邮箱地址
* @category 组织packages
* @copyright 指明版权信息
* @const 指明常量
* @deprecate 指明不推荐或者是废弃的信息
* @example 示例
* @exclude 指明当前的注释将不进行分析，不出现在文挡中
* @final 指明这是一个最终的类、方法、属性，禁止派生、修改。
* @global 指明在此函数中引用的全局变量
* @include 指明包含的文件的信息
* @link 定义在线连接
* @module 定义归属的模块信息
* @modulegroup 定义归属的模块组
* @package 定义归属的包的信息
* @param 定义函数或者方法的参数信息
* @return 定义函数或者方法的返回信息
* @see 定义需要参考的函数、变量，并加入相应的超级连接。
* @since 指明该api函数或者方法是从哪个版本开始引入的
* @static 指明变量、类、函数是静态的。
* @throws 指明此函数可能抛出的错误异常,极其发生的情况
* @todo 指明应该改进或没有实现的地方
* @var 定义说明变量/属性。
* @version 定义版本信息
*/
```
注释的信息很全面，可能有很多我们用不到，红色部分是我们经常用到的。  
# 示例`php`里面常见的几种注释方式：
### 1.文件的注释，介绍文件名，功能以及作者版本号等信息
```php
/**
* 文件名简单介绍
*
* 文件功能
* @author 作者
* @version 版本号
* @date 2020-02-02
*/
```
### 文件头部模板
```php
/**
*这是一个什么文件
*
*此文件程序用来做什么的（详细说明，可选。）。
* @author   richard<e421083458@163.com>
* @version   $Id$
* @since    1.0
*/
```
### 2.类的注释，类名及介绍
```php
/**
* 类的介绍
*
* 类的详细介绍（可选）
* @author 作者
* @version 版本号
* @date 2020-02-02
*/
```
```php
/**
* 类的介绍
*
* 类的详细介绍（可选。）。
* @author     richard<e421083458@163.com>
* @since     1.0
*/
class Test 
{
}
```
### 3.函数的注释，函数的作用，参数介绍以及返回类型
```php
/**
* 函数的含义说明
*
* @access public
* @author 作者
* @param mixed $arg1 参数一的说明
* @param mixed $arg2 参数二的说明
* @return array 返回类型
* @date 2020-02-02
*/
```
### 函数头部注释
```php
/**
* some_func
* 函数的含义说明
*
* @access public
* @param mixed $arg1 参数一的说明
* @param mixed $arg2 参数二的说明
* @param mixed $mixed 这是一个混合类型
* @since 1.0
* @return array
*/
public function thisIsFunction($string, $integer, $mixed) {return array();}
```
### 程序代码注释
1. 注释的原则是将问题解释清楚，并不是越多越好。  
2. 若干语句作为一个逻辑代码块，这个块的注释可以使用`/* */`方式。  
3. 具体到某一个语句的注释，可以使用行尾注释：`//`。  
```php
/* 生成配置文件、数据文件。*/
 
$this->setConfig();
$this->createConfigFile(); //创建配置文件
$this->clearCache();     // 清除缓存文件
$this->createDataFiles();  // 生成数据文件
$this->prepareProxys();
$this->restart();
```

# PHP命名规范

## 1.目录和文件
目录使用小写+下划线.  
类库，函数文件统一以.php为后缀.  
类的文件名均以命名空间定义，并且命名空间的路径和类库文件所在路径一致.  
类文件采用驼峰法命名（首字母大写），其他文件采用小写+下划线命名.  
类名和类文件名保持一致，统一采用驼峰法（首字母大写）.  

## 2.函数和类，属性命名
类的命名采用驼峰法（首字母大写），例如 `User`、`UserType`，默认不需要添加后缀，例如`UserController`应该直接命名为`User`
函数的命名使用小写字母和下划线（小写字母开头）的方式，例如 `get_client_ip`.  
方法的命名使用驼峰法（首字母小写），例如 `getUserName`(如果方法有返回值，那么目前习惯上将首字母用小写的属性类型，如s(`string`)，i(`int`)，f(`float`)，b(`boolean`)，a(`array`)等).  
属性的命名使用驼峰法（首字母小写），例如 `tableName`、`instance`（目前习惯上将首字母用小写的属性类型，如s(`string`)，i(`int`)，f(`float`)，b(`boolean`)，a(`array`)等）.  
以双下划线`“__”`打头的函数或方法作为魔法方法，例如 `__call` 和 `__autoload`  

## 3.常量和配置
常量以大写字母和下划线命名，例如 `APP_PATH`和 `THINK_PATH`
配置参数以小写字母和下划线命名，例如 `url_route_on`和`url_convert`

## 4.数据表盒字段
数据表和字段采用小写加下划线方式命名，并注意字段名不要以下划线开头，例如 `think_user` 表和 `user_name`字段，不建议使用驼峰和中文作为数据表字段命名。
