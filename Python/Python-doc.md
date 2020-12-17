## @property 和 @score.setter

@property 将方法变成属性

@score.setter 将方法变成属性赋值



## weakref  --- 弱引用

当对象只剩弱引用时，对象可以被回收。



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

