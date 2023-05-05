`Python` 是一门**动态**语言,任何时候都可以直接定义变量、函数等而无需标注类型。

```python
name = 'admin'

def hello():
		print('Hello')
```

`Python` 在 `3.5` 之后引入了类型注解, 可声明变量类型、函数入参类型和返回值类型等。

# 基本类型

## 整数 int 和浮点数 float

```python
a: int = 1
b: float = 1.0
```

## 字符串 str

```python
a: str = 'a string'
```

## 布尔值 bool

布尔值仅两个枚举值, `True` 和 `False`:

```python
a: bool = True
b: bool = False
```

## bytes

```python
a: bytes = b'32'
```

## 数组 List

使用方括号 `[]` 创建数组:

```python
a: list = [1, 2, 3]
```

## 元组 Tuple

> [!tip]
> 元组不可变 (`Immutable`)。

使用括号 `()` 创建元组:

```python
a: tuple = (1, 2, 3)
```

## 字典 Dict

> [!tip]
> 字典为键值对。

使用花括号 `{}` 创建字典:

```python
a: dict = {'name': 'admin'}
```

## 集合 Set

> [!tip]
> - 集合中元素不可重复;
> - 集合中元素是无序的。

```python
a: set = {1, 2, 3}
```

数组、元组、字典、集合和序列也可从 `typing` 引入:

```python
from typing import List, Tuple, Dict, Set, Sequence
```

## 空值 None

```python
a: None = None
```

## Any 类型

`Any` 类型可作为兜底类型:

```python
from typing import Any

a: Any = 1
b: Any = 1.0
c: Any = '1'
d: Any = True
```

## NoReturn

`NoReturn` 用于表示函数无返回值:

```python
from typing import NoReturn

def oh_no() -> NoReturn:
    raise RuntimeError('Oh No!')
```

在 `Python` 中函数如果无 `return` 语句, 那么会隐式返回一个 `None`, 如果不想让这种隐式行为发生, 则可以使用 `NoReturn`。

## 枚举 Enum

```python
from enum import Enum
 
class Season(Enum):
    SPRING = 1
    SUMMER = 2
    AUTUMN = 3
    WINTER = 4
 
# printing enum member as string
print(Season.SPRING) # Season.SPRING
 
# printing name of enum member using "name" keyword
print(Season.SPRING.name) # SPRING
 
# printing value of enum member using "value" keyword
print(Season.SPRING.value) # 1
 
# printing the type of enum member using type()
print(type(Season.SPRING)) # <enum 'Season'>
 
# printing enum member as repr
print(repr(Season.SPRING)) # <Season.SPRING: 1>
 
# printing all enum member using "list" keyword
print(list(Season)) # [<Season.SPRING: 1>, <Season.SUMMER: 2>, <Season.AUTUMN: 3>, <Season.WINTER: 4>]
```

# 类型别名 as

```python
from typing import Sequence as sequence_alias
```

# 可选类型 Optional

```python
from typing import Optional

a: Optional[int] = None
```

变量 `a` 被赋初值 `None`, 在这之后的任何时候 `a` 都可以被赋值为整数。

# 联合类型 Union

```python
from typing import Union

def foo(parameter: int) -> Union[str, int, float]:
    if (parameter == 1):
        return "one"
    elif (parameter == 2):
        return 2
    else:
        return 3.0
```

上述 `foo` 函数会根据入参值的不同而返回不同类型的值:
- 入参为 `1` 时返回字符串 `one`
- 入参为 `2` 时返回整数 `2`
- 入参为其他值时返回浮点数 `3.0`

> [!tip]
> `Option` 是 `Union` 的特例: Optional[T] 和 Union[T, None] 等价。

`Python 3.10` 及更高版本支持如下联合类型写法:

```python
def foo(parameter: int) -> str | int | float:
	...
```

# 可调用 Callable

只要给类实现了 `__call__` 方法, 那么这个类就是可调用的 (`Callable`):

```python
from typing import Callable

class Foo:
    def __call__(self):
        print('I am foo')

def bar():
    print('I am bar')


def hello(a: Callable):
    a()

# 类型检查通过
hello(Foo())
# 同样通过
hello(bar)
```

# Self

`Self` 用于在一个类的方法里标注返回值类型为这个类本身:

```python
from typing import Self

class Foo:
    def return_foo(self) -> Self:
        return self
```

[PEP 673 – Self Type](https://peps.python.org/pep-0673/)

```python
class Foo:
    def return_foo(self) -> "Foo":
        return self
```

# *args 和 **kwargs

# 判断变量类型

## type

```python
type(1) # <class 'int'>
type(1.0) # <class 'float'>
type('1') # <class 'str'>
type(True) # <class 'bool'>
type(False) # <class 'bool'>
type(None) # <class 'NoneType'>

type([]) # <class 'list'>
type(()) # <class 'tuple'>
type({}) # <class 'dict'>
type({1}) # <class 'set'>
```

可以使用 `__name__` 属性:

```python
type(1).__name__ # 'int'
type(1).__name__ == 'int' # True
```

## isinstance

```python
isinstance(1, int) # True
```