# PEP 8 Python 编码风格 -- what_pep8_says
PEP8 港了些撒？学习一波必不可少。


## 代码布局 Code Lay-out

### 缩进 indent

4个空格缩进。

函数参数可以折行，与上一行变量、名称、行首比，空4格，都可以。

```python
# Aligned with opening delimiter.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# Add 4 spaces (an extra level of indentation) to distinguish arguments from the rest.
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# Hanging indents should add a level.
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
```

### 空格还是tab？

空格。尤其不要 tab 和 空格 混用。

### 最大行长度

代码 79。宽屏可以到 99。

注释、docstring 应该 72

### 双目运算符前、还是后折行？

之前。前面更易读懂。

```python
# Yes: easy to match operators with operands
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
```

### 空行

最顶级函数、类，前后各空2行。

class 里的 方法，前后各空1行。

一组代码，可以用1行空行隔开。

### 源文件编码

UTF-8

### import

每个包要单独导入，不要一句话导入好几个包。

```python
Yes: import os
     import sys

No:  import sys, os
```

一个包的多个内容，可以一句话导入。

```python
from subprocess import Popen, PIPE
```

导入的包要在文件顶部，尽在模块注释、docstring之后，在全局变量、常数之前。

包要分类，用1行空行隔开：

1. 标准库最先
2. 三方库在后
3. 本程序特有库最后

不要用通配符导入包，类似这种：`from module import *` 会造成名称污染。

### 模块级的双下划线

`__all__`、`__author__`、`__version__` 这些，只在 `__future__` 后面，在其他 import 前面。

```python
"""This is the example module.

This module does stuff.
"""

from __future__ import barry_as_FLUFL

__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'

import os
import sys
```

## 字符串引号

单双引号一个样。可以互相嵌套。

三重引号要一直用双引号！（PEP257 载明）

## 语句、表达式里的空格

### pet peeves 萌宠皮皮？

括号内、括号间就不要空格了

```python
Yes: spam(ham[1], {eggs: 2})
No:  spam( ham[ 1 ], { eggs: 2 } )
```

结尾的逗号和括号间，不要空格

```python
Yes: foo = (0,)
No:  bar = (0, )
```

逗号，分号，冒号前，不要空格

```python
Yes: if x == 4: print x, y; x, y = y, x
No:  if x == 4 : print x , y ; x , y = y , x
```

切片的冒号两边，空格还是一致比较好

```python
# YES:
ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
ham[lower:upper], ham[lower:upper:], ham[lower::step]
ham[lower+offset : upper+offset]
ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
ham[lower + offset : upper + offset]

# NO:
ham[lower + offset:upper + offset]
ham[1: 9], ham[1 :9], ham[1:9 :3]
ham[lower : : upper]
ham[ : upper]
```

左括号前不留空格

```python
Yes: spam(1)
No:  spam (1)
# and []
Yes: dct['key'] = lst[index]
No:  dct ['key'] = lst [index]
```

赋值什么的等号两边不要多余的空格（不要用空格排版，不提高可读性）

```python
# Yes:
    x = 1
    y = 2
    long_variable = 3

# No:
    x             = 1
    y             = 2
    long_variable = 3
```

### 其他

- 任何地方都不需要行尾空格——看不着，就会有歧义。（例如行尾反斜杠 \ 后面如果有空格，到底是不是换行就不好说了，不同的解释器解释方法都不一样。）
- 赋值 `=` 、扩展赋值 `+=` `-=`  、比较`==` `<` `>` `!=` `<>` `<=` `>=` `in` `is` `is not` 、逻辑 `and` `or` `not` 两边**各1个**空格
- 不同优先级的运算符混用时，低优先级的运算符两边加空格，会易懂。

```python
# Yes:
i = i + 1
submitted += 1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)

# No:
i=i+1
submitted +=1
x = x * 2 - 1
hypot2 = x * x + y * y
c = (a + b) * (a - b)
```

- 函数注释的 `:` 和 `->` 规则同前，不需要紧凑。

```python
# Yes:
def munge(input: AnyStr):
def munge() -> PosInt:

# No:
def munge(input:AnyStr):
def munge()->PosInt:
```

- 函数带名字的形参赋值时，`=` 等号两边不要空格。

```python
# Yes:
def complex(real, imag=0.0):
    return magic(r=real, i=imag)

# No:
def complex(real, imag = 0.0):
    return magic(r = real, i = imag)
```

- 不建议一行写多句（用 ; 分隔的那种）

```python
# 坏例子:
if foo == 'blah': do_blah_thing()
do_one(); do_two(); do_three()
```

- 有时候在 if/for/while 同一行后面也可以放短小语句。但绝不要放复合句，更不要有长句，甚至作死的折行！

## 什么时候用结尾逗号

结尾的逗号一般是可选的，tuple 的话，要用 () 括起来。

```python
# Yes:
FILES = ('setup.cfg',)

# OK, but confusing:
FILES = 'setup.cfg',
```

用 list 或者 tuple 的时候，逗号后面折行比较方便增删内容。（上例中一个元素的 tuple `x = (A,)`除外）

```python
# Yes:
FILES = [
    'setup.cfg',
    'tox.ini',
    ]
initialize(FILES,
           error=True,
           )

# No: 不是不行，而是不方便
FILES = ['setup.cfg', 'tox.ini',]
initialize(FILES, error=True,)
```

## 注释

错误注释还不如没有。代码变化之后，一定要立即更新注释！

用完整的句子做注释。

不要改变标识符的大小写！

块状注释通常要有好几句/段，每句话要写句号。

每个句号之后，空两格。最后一句除外。

英文注释，按照 Strunk & White 的《写作要素》的要求写。（ps，值得另学）

非英语程序员，也要写英语注释——除非120%确信不会有其他国家人看。

### 块状注释

就是一些连在一起的 # 注释。通常用来注释后面同级的一块代码。每句话用 # 开头。

### 行内注释

节省点，别乱写。注释的 # 前面至少空2格，后面空1格。

行内注释不要描述显见的事情，会分散注意力。

```python
# YES:
x = x + 1                 # Compensate for border

# NO:
x = x + 1                 # Increment x
```

### docstrings

docstrings 在 PEP 257 里有明确标准。

公用模块、函数、类、方法，要写docstrings！不公用的不用写 docstrings，但在def 后面，还是要有注释这东西干嘛的！

多行的 docstrings，结尾的 三引号 单独一行。

```python
"""基本描述
详细情况 bla bla
"""
```

只有一行的三引号，结尾的三引号就不用独立了，例如： `"""bla bla"""`

## 命名

python 库的命名是一团糟，也很难统一，所以只能有点小建议。至少在命名新模块、包的时候，应该遵循这些标准。（现有库的命名有些不同的风格，为了保持稳定性，暂时不能动）

### 覆盖原则

作为公共 API 出现的名称，应该反应其用法，而非实现了什么。

### 命名风格：描述性

命名风格繁多，各不相同。常用的有：

- 小写单字母 b
- 大写单字母 B
- 小写 lowercase
- 小写加下划线 lower_case_with_underscores
- 大写 UPPERCASE
- 大写加下划线 UPPER_CASE_WITH_UNDERSCORES
- 首字母大写 CapitalizedWords
- 驼峰 mixedCase （首字母小写，中间大写）
- 大写加下划线——这个就很丑了！没事别自找不痛快。

也有用前缀的啊，例如 st_mode, st_size 表明 struct_mode, struct_size。

X11 的库前面还会用 X... 开头。

下划线开头、结尾的，有特定含义：

- `_single_leading_underscore` 下划线开头，表明是内部使用，import 时候，不会导入。
- `single_trailing_underscore_` 下划线结尾，用来防止和关键字冲突。例如 `Tkinter.Toplevel(master, class_='ClassName')`
- `__double_leading_underscore` 双下划线开头，命名类方法的时候，会变形。例如 class FooBar 里的 `_boo` 会变形为 `_FooBar__boo`
- `__double_leading_and_trailing_underscore__` 双下划线开头结尾，是魔术方法，例如：`__init__`, `__import__`, `__file__` 等。千万不要自己造这种命名，一定要按照文档给出的来用。

### 命名约定

#### 避免如下名字

别用 l(el) O(oh) I(eye) 这样的单字母命名。因为有些字体下 O0lI 这些分不清.

#### ascii兼容性

标识符一定要用标准 ascii 码。详情可以看 PEP 3131。

#### 包、模块名

模块用简短、全小写的名字，可以用下划线。

包也是简短全小写名字，但不建议用下划线。

当用C/C++写了高阶（例如更加面向对象）的接口时，C/C++模块用下划线开头，例如 `_socket`

#### 类名 class

类名首字母大写。

python 内建的包是1-2个小写单词构成的，但自己的包不可以这样命名。

#### 类型变量名

PEP 484 引入的类型变量，一般用首字母大写：`T, AnyStr, Num`, 也建议加上尾缀 `_co` 或者 `_contra` 。

```python
from typing import TypeVar

VT_co = TypeVar('VT_co', covariant=True)
KT_contra = TypeVar('KT_contra', contravariant=True)
```

#### 异常 exception 名

虽然 exception 是类，但是要用 `Error` 异常

#### 全局变量名

首先：假定这些变量只在本模块用。

其次：函数的命名方式一样的。

模块用 `__all__` 机制来防止 `from M import *` 时全局变量干扰。（古方就不提也罢）

#### 函数及变量名

函数名要小写，适时加下划线。

变量名同上。

驼峰等命名法，仅用在已流行的的用法上，例如 threading.py，以保持前向兼容性。自己新写的不要驼峰。

#### 函数及方法的参数

实例方法的第一个参数是 self。

类方法第一个参数时 cls。

如果函数参数名与保留字冲突，后面加一个下划线，比用其他缩写或拼写更好：例如 `class_` 要比 `clss` 就好。（当然，用同义词也许是更好的办法）

#### 方法名、实例变量名

同函数命名规则：小写，加必要的下划线，以便阅读。

非共有方法、变量前加一个下划线。

为防止子类名称冲突，可以用双下划线开头——利用python的名称变形规则。（class Foo 里的 `__a` 只能通过 `Foo._Foo__a` 访问。通常，双下划线开头的变量仅用于子类的防止名称冲突。

#### 常量

常量通常定义为模块级的，大写，加下划线。例如 `MAX_OVERFLOW`，`TOTAL`

#### 继承的设计

设计类方法和实例变量（更准确说是：属性）时，就要考虑是公开变量还是非公开变量。如果不确定，选择非公开。后期将非公开变量公开，要比公开变量改为不公开更容易。

公开属性是公布出来给别人用的，不应该有后向兼容性变化。非公开变量是不打算给第三方使用的，无需刻意保持不变，甚至将来取消都可以。

这里没用“私有”这个说法，因为python中没有谁可用真的私有化（需要大量不必要的工作量）

子类的API，其他语言通常叫做 protected 类型。有些类被设计为基类，供其他类继承。设计这种类的时候，要尤其搞清楚哪些是要公开的（这些将成为子类的API），那些仅供基类自用。

如是我闻：

- 公开属性名不以下划线开头
- 公开属性名与保留字冲突时，末尾加下划线。（然，类方法的 `cls` 就习惯上这么用）
- 为简化类数据属性，最好只暴露属性名，不要暴露那些存取器什么的方法。需要函数处理的情况，就用 @property 这种，隐藏存取细节。
  1. 注1：属性 @property 仅限于新式类可用
  2. 注2：尽量避免函数的副作用——虽然缓存这类的副作用通常也可以接受。
  3. 注3：**避免把计算密集型的操作定为属性**，调用的人很容易以为调用并不费计时！
- 如果类作为基类，但是有些属性又不希望被继承，那么用双下划线开头，这样可以利用python的名称混淆机制，来避免子类和父类属性名冲突。
  - 注1：只有简单的类名才用到混淆机制，所以如果子类选择相同的类名、属性名，还是会造成明明冲突的。
  - 注2：名称混淆有特定用处，例如 debug 和 `__getattr()__` 。
  - 不是人人都喜欢名称混淆，所以要权衡普通用户和高级用户的平衡。

### 公共及内部接口

后向兼容只针对公开接口。所以，用户要能够清晰区别公开接口和内部接口。

除非明确指出是内部接口，文档载明的应视为公开接口；未载明的都视为内部接口。

为更好的支持内省，模块应用 `__all__` 公开API。如 `__all__` 为空，则模块没有公开的API。

即便正确设置了 `__all__` ，内部接口（包、模块、类、函数、方法或其他变量）仍应用下划线开头。

导入的名称总应该视为实现的细节（？），其他模块绝不应间接依赖于非明确公开的导入名称，如 `os.path` 或者某个包里的 `__init__` 模块，就不应暴露给子模块。

## 编程建议

- 编写的代码绝不要对其他python实现造成不好的影响（如 PyPy, Jython, IronPython, Cython, Psyco 等）。

  例如，不能依赖于 CPython 高效的 in place 字符串连接语句，如 `a += b` 或者 `a = a + b` 。这种优化很脆弱，即便 CPython 中也只有部分类型可用，而且不是并不是所有实现都支持。更好的解决方式应该是 `''.join()` 。join 方法可用保证所有的实现方法里，字符串连接耗时都是线性的。

- 与 `None` 这种单例比较，一定要用 `is` 或 `is not`，绝不要用等号！

  且，应注意，写 `if x` 而实际上意思是 `if x is not None` 这种时，变量或参数默认是 None 但设为其他值，其他值也许有类型（例如容器），测试逻辑值就不是False 了。

- 用 `is not` ，而非 `not ... is` 。虽然意义相同，前者更易懂，推荐。

```python
# Yes:
if foo is not None:

# No:
if not foo is None:
```

- 当【不大理解】咋咋咋比较复杂类型时，最好实现 `__eq__`, `__ne__`, `__lt__`, `__le__`, `__gt__`, `__ge__` 这6个操作符，比乱七八糟的比较要好。

  为减小影响，`functools.total_ordering()` 提供了缺失的比较方法。

  PEP 207 指明。。。。【不好翻，不写了】

- 要用 `def` 来定义函数，不要用 lambda 函数喽。

```python
# Yes:
def f(x): return 2*x

# No:
f = lambda x: 2*x
```

def f(x) 这种，明确定义了一个函数，而lambda表达式返回一个通用的 `<lambda>` 。在出错回溯的时候，函数有优势。

- 从 `Exception` 继承异常，不要从 `BaseException` 继承。基本上，从 `BaseException` 继承的，都是错误的。

  设计异常层次时候，抓到异常代码比异常位置重要，要关心 “什么出错了？”，而不要只生成 “出错了！” 这样的信息（见 PEP 3151）。

  命名异常时候，用类命名方法，前面加 Error开头。不是错误的异常，用于非本地流程控制，或者用其他信号？？【又是翻不清楚】

- 正确使用异常链。使用 `raise X from Y` ，能明确追溯到源位置。
- 捕获异常时，要给出具体什么异常，不能只用一个 `except` 子句：

```python
try:
    import platform_specific_module
except ImportError:
    platform_specific_module = None
```

只用 `except` 捕捉，就会拦截系统退出 SystemExit 和键盘中断 KeyboardInterrupt 异常，程序将难以用 Control-C 中断，还会掩盖其他问题。如果只是想捕捉所有程序错误，用 `except Exception:` （相当于 `except BaseException:` ）。

用以下2种方法，节俭使用 `except`

  1. print 或者 log 显示错误，这样用户就知道出错了；
  2. 如果代码需要清理，这时候把异常转为 `raise.try ... finally` 这种比较有效。

- 当给绑定的异常起名字的时候，给绑定个好名字呗。

```python
try:
    process_data()
except Exception as exc:
    raise DataProcessingFailedError(str(exc))
```

- 捕捉系统异常时，用 `errno`
- 所有的 try/except 语句，`try` 中语句要**尽可能**最少，防止掩盖其他bug

```python
# Yes:
try:
    value = collection[key]
except KeyError:
    return key_not_found(key)
else:
    return handle_value(value)

# No:
try:
    # Too broad!
    return handle_value(collection[key])
except KeyError:
    # Will also catch KeyError raised by handle_value()
    return key_not_found(key)
```

- 当某一资源只在本地局部使用，用 `with` 包围起来，以确保用后立即释放。用 try/finally 也可接受。
- 当申请、释放资源的时候，用上下文管理器（with），包裹单独的函数或方法来申请。

```python
# Correct(用的函数、方法):
with conn.begin_transaction():
    do_stuff_in_transaction(conn)

# Wrong(用错了！):
with conn:
    do_stuff_in_transaction(conn)
```

后面这个错误的例子，因为不可能提供 `__enter__` 和 `__exit__` 这类方法，也就没可能在会话结束后释放资源。

- 函数的返回语句 `return` 要一致。一个函数的出口，要么都返回值或者表达式，要么都不返回。如果遇到没有值可 return 的情况，用 `return None` 。如果可行，return 应该在函数的最后面。

```python
# Correct 最优雅:
def foo(x):
    if x >= 0:
        return math.sqrt(x)
    else:
        return None

# Correct 也还不错（也有优化建议是及早把特例短路掉）:
def bar(x):
    if x < 0:
        return None
    return math.sqrt(x)

# Wrong 有的情况没有 return:
def foo(x):
    if x >= 0:
        return math.sqrt(x)

# Wrong 有的 return 没有值:
def bar(x):
    if x < 0:
        return
    return math.sqrt(x)
```

- 字符串查找前、后缀时，用 `''.startswith()` 和 `''.endwith()` ，不要用切片。这两个函数更清晰不易出错。

```python
# Correct:
if foo.startswith('bar'):

# Wrong:
if foo[:3] == 'bar':
```

- 比较变量、对象类型时，用 `isinstance()` ，别用 type() 比较。

```python
# Correct:
if isinstance(obj, int):

# Wrong:
if type(obj) is type(1):
```

- 对序列 (string, list, tuple) 而言，空序列是 False：

```python
# Correct:
if not seq:
if seq:

# Wrong:
if len(seq):
if not len(seq):
```

- 别让字符串依赖于尾部的空格，因为尾部空格可能会被编辑器或者缩进工具删掉。
- 别用等于 `==` 比较逻辑值的真伪！

```python
# Correct: 这个好！
if greeting:

# Wrong: 错的！
if greeting == True:

# Worse: 错得离谱！
if greeting is True:
```

- 不鼓励在 `try ... finally` 里使用流程控制语句，如 `return/break/continue` ，让流程跳到 `finally` 之外。这样会在 finally 中取消前面的异常。

```python
# Wrong:
def foo():
    try:
        1 / 0
    finally:
        return 42    # 掩盖了前面的异常，不鼓励
```

### 函数释文

PEP 484 说了，函数释文规则依 484 为准，PEP 8 的不算数了。

### 变量释文

PEP 526 为准。

- 模块级变量、类和实例变量、本地变量：冒号后空1格。
- 冒号前不空格
- 赋值语句，等号两边各1个空格。

```python
# Correct:
code: int

class Point:
    coords: Tuple[int, int]
    label: str = '<unknown>'

# Wrong:
code:int  # No space after colon
code : int  # Space before colon

class Test:
    result: int=0  # No spaces around equality sign
```
