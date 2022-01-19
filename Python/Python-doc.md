## @property 和 @x.setter -- 方法变成属性

@property 将方法变成属性

@x.setter 将方法变成属性赋值

```python
In [22]: class test:
    ...:     data = 1
    ...:     @property
    ...:     def a(self):
    ...:         return self.data
    ...:     @a.setter
    ...:     def a(self, value):
    ...:         self.data = value
    ...:

In [23]: t = test()

In [24]: t.a
Out[24]: 1

In [25]: t.a = 2

In [26]: t.a
Out[26]: 2

In [27]: t.a += 4

In [28]: t.a
Out[28]: 6
```



## weakref  --- 弱引用

当对象只剩弱引用时，对象可以被回收。

```python
In [1]: import weakref

In [2]: class test:
   ...:     pass
   ...:

In [3]: t = test()

In [4]: r = weakref.ref(t)

In [5]: a = r()

In [6]: a is t
Out[6]: True

In [7]: del t

In [17]: print(r())
<__main__.test object at 0x7fec9eec45b0>

In [18]: del a

In [19]: print(r())
None

In [20]:
```

#### weakref.finalize 终结器

```python
In [42]: import weakref

In [43]: class test:
    ...:     pass
    ...:

In [44]: t = test()

In [45]: weakref.finalize(t, print, "testtest")
Out[45]: <finalize object at 0x7fec9ee1f390; for 'test' at 0x7fec9eeeef10>

In [46]: del t
testtest

In [47]:
```



## \_\_slots\_\_  --- 预先声明实例属性

通过预先声明实例属性等对象并移除实例字典来节省内存

继承多个父类时\_\_slots\_\_不能合并，会抛出异常。

```python
In [93]: class test2:
    ...:     __slots__=('t2')
    ...:

In [94]: class test:
    ...:     __slots__=('t')
    ...:

In [95]: class test3(test, test2):
    ...:     pass
    ...:
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-95-1d6f84490262> in <module>
----> 1 class test3(test, test2):
      2     pass
      3

TypeError: multiple bases have instance lay-out conflict

In [96]:
```



## singledispatch -- 泛型函数

functools.singledispatch **3.4**

```python
In [7]: from functools import singledispatch

In [8]: @singledispatch
   ...: def fun(arg):
   ...:     print(f'fun:{arg}')
   ...:

In [9]: @fun.register
   ...: def _(arg:int):
   ...:     print(f'int:{arg}')
   ...:

In [10]: @fun.register
    ...: def _(arg:str):
    ...:     print(f'str:{arg}')
    ...:

In [11]: fun(1)
int:1

In [12]: fun('2')
str:2
```



## singledispatchmethod -- 泛型方法

functools.singledispatchmethod  **3.8 **

```python
In [1]: from functools import singledispatchmethod

In [3]: class test:
   ...:     @singledispatchmethod
   ...:     def fun(self, args):
   ...:         print(f'fun:{args}')
   ...:     @fun.register
   ...:     def _(self, arg:str):
   ...:         print(f'str:{arg}')
   ...:     @fun.register
   ...:     def _(self, arg:int):
   ...:         print(f'int:{arg}')
   ...:

In [4]: a = test()

In [5]: a.fun(1)
int:1

In [6]: a.fun('1')
str:1
```



## \_\_enter\_\_ 和 \_\_exit\_\_

```python
In [79]: class Lock:
    ...:     def __enter__(self):
    ...:         print("lock")
    ...:     def __exit__(self,exc_type, exc_val, exc_tb):
    ...:         print("unlock")
    ...:         print(exc_type)
    ...:         print(exc_val)
    ...:         print(exc_tb)
    ...:
    ...:

In [81]: with Lock() as lock:
    ...:     print("start")
    ...:     raise Exception('11')
    ...:
    ...:
lock
start
unlock
<class 'Exception'>
11
<traceback object at 0x7ff9c3d5ea80>
---------------------------------------------------------------------------
Exception                                 Traceback (most recent call last)
<ipython-input-81-20aecf6c19d5> in <module>
      1 with Lock() as lock:
      2     print("start")
----> 3     raise Exception('11')
      4
      5

Exception: 11

In [82]:
```



## functools.wraps

保留原函数的名称和函数属性

```python
In [15]: import functools

In [16]: def test(func):
    ...:     @functools.wraps(func)
    ...:     def test2():
    ...:         func()
    ...:         return ''
    ...:     return test2
    ...:

In [17]: @test
    ...: def test3():
    ...:     pass
    ...:

In [18]: test3.__name__
Out[18]: 'test3'

In [19]:
```



## nest_asyncio 

python 交互式解释器使用 asyncio 会出现以下错误

`RuntimeError: This event loop is already running`

安装nest_asyncio解决

```python
import nest_asyncio
nest_asyncio.apply()
```



## metaclass -- 元类

```python

In [51]: class Mymeta(type):
    ...:     def __init__(self, name, bases, dic):
    ...:         super().__init__(name, bases, dic)
    ...:         print('====Mymeta.__init___')
    ...:         print(self.__name__)
    ...:         print(dic)
    ...:         print(self.yaml_tag)
    ...:     def __new__(cls, *args, **kwargs):
    ...:         print('===>Mymeta.__new__')
    ...:         print(cls.__name__)
    ...:         return type.__new__(cls, *args, **kwargs)
    ...:     def __call__(cls, *args, **kwargs):
    ...:         print('===>Mymeta.__call__')
    ...:         obj = cls.__new__(cls)
    ...:         cls.__init__(cls, *args, **kwargs)
    ...:         return obj
    ...:

In [52]: class Foo(metaclass=Mymeta):
    ...:     yaml_tag = '!Foo'
    ...:     def __init__(self, name):
    ...:         print('Foo.__init__')
    ...:         self.name = name
    ...:     def __new__(cls, *args, **kwargs):
    ...:         print('Foo.__new__')
    ...:         return object.__new__(cls)
    ...:
===>Mymeta.__new__
Mymeta
====Mymeta.__init___
Foo
{'__module__': '__main__', '__qualname__': 'Foo', 'yaml_tag': '!Foo', '__init__': <function Foo.__init__ at 0x7fc941f75790>, '__new__': <function Foo.__new__ at 0x7fc941f759d0>}
!Foo

In [53]: Foo(1)
===>Mymeta.__call__
Foo.__new__
Foo.__init__
Out[53]: <__main__.Foo at 0x7fc941f970d0>
```

\_\_new\_\_:
　　Called to create a new instance of class cls
\_\_init\_\_:
　　Called when the instance is created.



## \_\_call\_\_

重载()方法

```python
In [34]: class test:
    ...:     def __init__(self):
    ...:         self.name='test name'
    ...:     def run(self):
    ...:         print('run')
    ...:     def __call__(self):
    ...:         print('__call__')
    ...:

In [35]: t = test()

In [36]: t()
__call__

In [37]: hasattr(t.name, '__call__')
Out[37]: False

In [38]: hasattr(t.run, '__call__')
Out[38]: True

In [39]: def func():
    ...:     pass
    ...:

In [40]: hasattr(func, '__call__')
Out[40]: True

In [41]:
```



## copy -- 浅层 (shallow) 和深层 (deep) 复制操作

```python
In [84]: import copy

In [85]: class test:
    ...:     def __init__(self):
    ...:         self.name = 'test name'
    ...:     def __copy__(self):
    ...:         print('__copy__')
    ...:         return self
    ...:     def __deepcopy__(self, t):
    ...:         print(f'__deepcopy__: {t}')
    ...:         t = test()
    ...:         t.name = self.name
    ...:         return t
    ...:

In [86]: t = test()

In [87]: t1 = copy.copy(t)
__copy__

In [88]: t2 = copy.deepcopy(t)
__deepcopy__: {}

In [89]: t2
Out[89]: <__main__.test at 0x7fec9f0b34f0>

In [90]: t2.name
Out[90]: 'test name'

In [91]: t1.name
Out[91]: 'test name'

In [92]: t.name
Out[92]: 'test name'

In [93]: t.name = '1111'

In [94]: t1.name
Out[94]: '1111'

In [95]: t2.name
Out[95]: 'test name'

In [96]:
```



## enum 枚举

#### IntFlag 可以使用位运算符

```python
In [162]: from enum import IntFlag

In [163]: class Perm(IntFlag):
     ...:     R = 4
     ...:     W = 2
     ...:     X = 1
     ...:

In [164]: type(Perm.R | Perm.W)
Out[164]: <enum 'Perm'>

In [165]: RW = Perm.R | Perm.W

In [166]: Perm.R in RW
Out[166]: True

```



## struct --- 将字节串解读为打包的二进制数据





## 新式类和经典类

2.x版本默认经典类，3.x只有新式类

**MRO**(基类搜索顺序): 经典类**从左到右深度优先**搜索, 新式类**从左到右广度优先**搜索

```python
In [38]: class A:
    ...:     def nmae(self):
    ...:         print('A')
    ...:

In [39]: class B(A):
    ...:     pass
    ...:

In [40]: class C(A):
    ...:     def name(self):
    ...:         print('C')
    ...:

In [41]: class D(B,C):
    ...:     pass
    ...:

In [42]: d = D()

In [43]: d.name()
C
```



## eval、exec、complie

eval:  执行单个python表达式，返回改表达式的值

exec: 可执行复杂代码块，无返回值

complie:

