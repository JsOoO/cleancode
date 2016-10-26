##后端编码规范

本篇是后端编码规范（以php为主要语言），根据PSR编码标准起草，根据实际情况略有改动，详细请戳[链接](https://psr.phphub.org/)

###一、PSR-1--基础编码规范
####1.概览

- PHP代码文件 **必须** 以 `<?php` 标签开始，且 **一定不可** 写 `?>` 结束符；
- PHP代码文件 **必须** 以 不带 BOM 的 UTF-8 编码；
- PHP代码中 **应该** 只定义类、函数、常量等声明，或其他会产生 **副作用** 的操作（如：生成文件输出以及修改 .ini 配置文件等），二者只能选其一；
- 命名空间以及类 **必须** 符合 PSR 的自动加载规范：[PSR-4](https://psr.phphub.org/) 中的一个；
- 类的命名 **必须** 遵循 **FirstClass** 大写开头的驼峰命名规范；
- 类中的常量所有字母都 **必须** 大写，单词间用下划线分隔；
- 方法名称 **必须** 符合 **secondFunction** 式的小写开头驼峰命名规范；
> 以上，类、方法、变量、常量的命名 **应该** 使用 **名词** 或者 **名词+动词** 的表达清晰的 **陈述性短语** 进行命名。

####2.解释
#####2.1 副作用
「副作用」(side effects) 一词的意思是，仅仅通过包含文件，不直接声明类、函数和常量等，而执行的逻辑操作。
「副作用」包含却不仅限于：

- 生成输出
- 直接的 require 或 include
- 连接外部服务
- 修改 ini 配置
- 抛出错误或异常
- 修改全局或静态变量
- 读或写文件等
```php
<?php
// 「副作用」：修改 ini 配置
ini_set('error_reporting', E_ALL);

// 「副作用」：引入文件
include "file.php";

// 「副作用」：生成输出
echo "<html>\n";

// 声明函数
function foo()
{
	// 函数主体部分
}
```
> 上面是一个反例，既有副作用代码又有声明代码

#####2.2 类中常量
- 必须全部大写，单词之间使用下划线分隔
```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```
#####2.3 类中属性以及方法
- 类中属性以及方法统一使用小写字母开头的驼峰式命名
```php
<?php
class Foo
{
	public $fooBar;
	public function strToTime()
	{
		// TODO: do someting
	}
}
```
###二、PSR-2--编码风格规范
####1. 概览
- 代码 **必须** 遵循 [PSR-1](https://laravel-china.org/topics/2078) 中的编码规范 。
- 代码 **必须** 使用4个空格符而不是「Tab 键」进行缩进。
- 每行的字符数 **应该** 软性保持在 80 个之内，理论上 **一定不可** 多于 120 个，但 **一定不可** 有硬性限制。
- 每个 `namespace` 命名空间声明语句和 `use` 声明语句块后面，**必须** 插入一个空白行。
- 类的开始花括号 `{` **必须** 写在函数声明后自成一行，结束花括号 `}` 也 **必须** 写在函数主体后自成一行。
- 方法的开始花括号 `{` **必须** 写在函数声明后自成一行，结束花括号 `}` 也 **必须** 写在函数主体后自成一行。
- 类的属性和方法 **必须** 添加访问修饰符（`private`、`protected` 以及 `public`），`abstract` 以及 `final` **必须** 声明在访问修饰符之前，而 `static` **必须** 声明在访问修饰符之后。
- 控制结构的关键字后 **必须** 要有一个空格符，而调用方法或函数时则 **一定不可** 有。
- 控制结构的开始花括号 `{` **必须** 写在声明的同一行，而结束花括号 `}` **必须** 写在主体后自成一行。
- 控制结构的开始左括号后和结束右括号前，都 **一定不可** 有空格符；
- 每个函数长度 **应该** 控制在40行以内，过长的函数务必考虑拆分；
- **一定不可** 使用 `var` 定义变量。
####2. 解释
#####2.1 例子
以下是完全符合要求的示例代码：
```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // 方法的内容
    }
}
```
#####2.2 文件
- 所有PHP文件 **必须** 使用 `Unix LF (linefeed)` 作为行的结束符。
- 所有PHP文件 **必须** 以一个空白行作为结束。
- 纯PHP代码文件 **必须** 省略最后的 `?>` 结束标签。

#####2.3 行
- 行的长度 **一定不可** 有硬性的约束。
- 软性的长度约束 **必须** 要限制在 120 个字符以内，若超过此长度，带代码规范检查的编辑器 **必须** 要发出警告，不过 **一定不可** 发出错误提示。
- 每行 **不该** 多于80个字符，大于80字符的行 **应该** 折成多行。
- 非空行后 **一定不可** 有多余的空格符。
- 空行 **可以** 使得阅读代码更加方便以及有助于代码的分块。
- 每行 **一定不可** 存在多于一条语句。

#####2.4 缩进
代码 **必须** 使用4个空格符的缩进，**一定不可** 用 tab键。
> 备注：使用空格而不是「tab键缩进」的好处在于， 避免在比较代码差异、打补丁、重阅代码以及注释时产生混淆。 并且，使用空格缩进，让对齐变得更方便。

#####2.5 关键字 以及 True/False/Null
PHP所有 [关键字](http://php.net/manual/en/reserved.keywords.php) **必须** 全部小写。
常量 `true` 、`false` 和 `null` 也 必须 全部小写。
#####2.6 方法以及参数
- 所有方法都 **必须** 添加访问修饰符。
- 方法名称后 **一定不可** 有空格符，其开始花括号 **必须** 独占一行，结束花括号也 **必须** 在方法主体后单独成一行。参数左括号后和右括号前 **一定不可** 有空格。
- 一个标准的方法声明可参照以下范例，留意其括号、逗号、空格以及花括号的位置。
- 参数列表中，每个逗号后面 **必须** 要有一个空格，而逗号前面 **一定不可** 有空格。
- 有默认值的参数，**必须** 放到参数列表的末尾。

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

参数过多可以折行，如下：

```php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz(
	    $arg1,
	    &$arg2,
	    $arg3 = []
	) {
        // method body
    }
}
```

#####2.7 abstract 、 final 、 以及 static
需要添加 `abstract` 或 `final` 声明时，**必须** 写在访问修饰符前，而 `static` 则 **必须** 写在其后。

```php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```

####3. 控制结构

控制结构的基本规范如下：
- 控制结构关键词后 **必须** 有一个空格。
- 左括号 `(` 后 **一定不可** 有空格。
- 右括号 `)` 前也 **一定不可** 有空格。
- 右括号 `)` 与开始花括号 `{` 间 **必须** 有一个空格。
- 结构体主体 **必须** 要有一次缩进。
- 结束花括号 `}` **必须** 在结构体主体后单独成行。
> 每个结构体的主体都 **必须** 被包含在成对的花括号之中， 这能让结构体更加结构话，以及减少加入新行时，出错的可能性。 

#####3.1. if 、elseif 和 else#
标准的 `if` 结构如下代码所示，请留意「括号」、「空格」以及「花括号」的位置， 注意 `else` 和 `elseif` 都与前面的结束花括号在同一行。

```php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```
**应该** 使用关键词 `elseif` 代替所有 `else if` ，以使得所有的控制关键字都像是单独的一个词。

#####3.2. switch 和 case
标准的 `switch` 结构如下代码所示，留意括号、空格以及花括号的位置。 `case` 语句 **必须** 相对 `switch` 进行一次缩进，而 `break` 语句以及 `case` 内的其它语句都 **必须** 相对 `case` 进行一次缩进。

如果存在非空的 `case` 直穿语句，主体里 必须 有类似 `// no break` 的注释。
```php
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
```
#####3.3. while 和 do while
一个规范的 while 语句应该如下所示，注意其「括号」、「空格」以及「花括号」的位置。
```php
<?php
while ($expr) {
    // structure body
}
```
标准的 `do while` 语句如下所示，同样的，注意其「括号」、「空格」以及「花括号」的位置。
```php
<?php
do {
    // structure body;
} while ($expr);
```

#####3.4 for
标准的 `for` 语句如下所示，注意其「括号」、「空格」以及「花括号」的位置。
```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

#####3.5 foreach
标准的 `foreach` 语句如下所示，注意其「括号」、「空格」以及「花括号」的位置。
```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

#####3.6 try, catch
标准的 `try catch` 语句如下所示，注意其「括号」、「空格」以及「花括号」的位置。
```php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```

###三、编码习惯
每个人编码习惯不尽相同，为了方便项目代码的迭代，维护以及重构，成员编码习惯应该统一起来。
- 一个函数的长度 **不该** 超过40行，超过应考虑拆分，一个函数最好只负责一小块工作，然后根据工作命名，函数保持单一职责；
- 任何时候都 **一定不可** 以任何理由使用类似 `temp`, `a`, `b` 等毫无可读性的命名；
- 类、变量、函数 **应该** 使用语义表达清晰的命名，大多数情况下，变量名应该是 **名词** ，函数名应是 **动词** ，类名应是一类 **事物** 的名字，应该让代码 **“读”** 起来就像自然语言一样；
- **编码语义化**，让看代码的人在 **没有注释** 的情况下也能一眼看过去就知道实现了什么功能，功能有什么样的逻辑，逻辑处理了哪些数据；
- 编码过程中使用 **设计模式** ，**设计模式** 能大大提高变成开发效率，提高复用性，解耦；
- 编码过程中不要想着留个坑以后再处理（一般情况下，以后也懒得处理了），代码首先要自己看得下去；
- 同一个变量 **一定不可** 使用在意义不同的 **两个地方** ；
- 代码中尽量不要直接出现 **数字** ，应使用 **宏定义** 或者 **静态变量** 替代，目的是增强可读性，以及方便维护；
- 进行条件判断的时候，尽量使用 `if (50 == $number) {}` 这种方式，能避免 `if ($number = 50) {}` 这样的bug。
####1.实例
#####1.1 编码语义化 以及 函数单一职责
```php
<?php
namespace App\Logic\My;

use App\Logic\Order as OrderLogic;

class Order
{
	private $_userId;
	public function __construct($userId)
	{
		$this->_userId = $userId;
	}
	public function getOrderDetail($orderId)
	{
		$orderLogic = new OrderLogic($orderId);
		if (!$orderLogic->isMyOrder($this->_userId)) {
			echo '不是你的订单';
		}
		return $orderLogic->getDetail();
}

$myOrderLogic = new Order($userId);
$myOrderLogic->getOrderDetail($orderId);
```

#####1.2 变量使用
反例：
```php
<?php
$list = getAppleList();
foreach ($list as $k => $v) {
	$a = $v + 1;
	$list[$k] = $a;
}

$list = getOrangeList();
foreach ($list as $k => $v) {
	$a = $v + 1;
	$list[$k] = $a;
}
```
> 不同的两个地方使用了同一个变量，虽然不会有bug，但是代码读起来一团糟；使用了毫无意义的临时变量，阅读起来看不明白 `$a = $v + 1`这一步有什么意义。

#####1.3 代码中数字使用宏定义或者静态变量替代
coding过程中难免会出现数字的情况，为了阅读、维护方便，需要替换成静态值。

```php
<?php
define('NOW_TIME', $_SERVER['REQUEST_TIME']);

class Define
{
	//注意：静态变量赋值时，一定不能const ONE_DAY_SECONDS = 24 * 60 * 60这样
	const ONE_DAY_SECONDS = 86400; // one day seconds = 24 * 60 * 60s
}

setExpireTime(NOW_TIME + Defind::ONE_DAY_SECONDS);
```

###总结
以上，是我结合PHP PSR规范，以及自己工作中心得的一些总结。
代码能工作还不够，能工作的代码经常引起bug。满足于仅仅让代码能工作的程序员不够专业。如果说害怕没时间改进代码的结构和设计，我不敢苟同。没什么能比糟糕的代码给开发项目带来更深远和长期的损害了。进度可以修改，需求可以重新定义。但糟糕的代码只会一直腐败发酵，拖着团队的后腿。如果一个团队蹒跚前进，仅仅是因为匆匆的搞出一片代码沼泽，是不是有些太不值当。
当然了，糟糕的代码可以清理，只不过成本高昂。随着不好的代码沉淀下去，模块之间相互渗透，出现大量隐藏纠结的依赖关系，清理时找到陈旧的依赖关系又费时又费力。相反，保持代码整洁相对容易，早晨制造一片混乱，下午就能轻易地打扫干净，更好的是尽量编码的时候就边写边清理这是非常容易的。
所以，解决的方法就是保持代码的整洁和简单，不让代码腐败有机会开始。
> 推荐各位看一本书，Robert C. Martin 的 Clean code，整本书讲解了我们为什么要规范写代码这件看起来不大不小的事儿，以及如何优化自己的代码。看完之后我不仅规范了编码习惯，还渐渐的意识到“编程思维”这个东西，写代码不像是在完成一份工作，更像是在打磨一件艺术品，把代码整洁这件“小”事做到极致，也有另一番风味。

