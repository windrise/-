# python装饰器

## 1. 闭包函数

　　在看装饰器之前，我们先来搞清楚什么是闭包函数。python是一种面向对象的编程语言，在python中一切皆对象，这样就使得变量所拥有的属性，函数也同样拥有。这样我们就可以理解在函数内创建一个函数的行为是完全合法的。这种函数被叫做内嵌函数，这种函数只可以在外部函数的作用域内被正常调用，在外部函数的作用域之外调用会报错，例如：

　　　　　　 ![img](https://images2017.cnblogs.com/blog/1251096/201710/1251096-20171028145152195-1360676939.png)

而如果内部函数里引用了外部函数里定义的对象（甚至是外层之外，但不是全局变量），那么此时内部函数就被称为**闭包函数**。闭包函数所引用的外部定义的变量被叫做**自由变量**。闭包从语法上看非常简单，但是却有强大的作用。**闭包可以将其自己的代码和作用域以及外部函数的作用结合在一起**。下面给出一个简单的闭包的例子：

```
def count():
    a = 1
    b = 1
    def sum():
        c = 1
        return a + c  # a - 自由变量
    return sum
```

**总结** ：什么函数可以被称为闭包函数呢？主要是满足两点：函数内部定义的函数；引用了外部变量但非全局变量。



## 2. python装饰器

　　有了闭包函数的概念，我们再去理解装饰器会相对容易一些。**python装饰器本质上就是一个函数，它可以让其他函数在不需要做任何代码变动的前提下增加额外的功能，装饰器的返回值也是一个函数对象（函数的指针）**。装饰器函数的外部函数传入我要装饰的函数名字，返回经过修饰后函数的名字；内层函数（闭包）负责修饰被修饰函数。从上面这段描述中我们需要记住装饰器的几点属性，以便后面能更好的理解：

    * 实质： 是一个函数


    * 参数：是你要装饰的函数名（并**非函数调用**）


    * 返回：是装饰完的函数名（也**非函数调用**）


    * 作用：为已经存在的对象添加额外的功能


    * 特点：不需要对对象做任何的代码上的变动

python装饰器有很多经典的应用场景，比如：插入日志、性能测试、事务处理、权限校验等。装饰器是解决这类问题的绝佳设计。并且从引入中的列子中我们也可以归纳出：**装饰器最大的作用就是对于我们已经写好的程序，我们可以抽离出一些雷同的代码组建多个特定功能的装饰器，这样我们就可以针对不同的需求去使用特定的装饰器，这时因为源码去除了大量泛化的内容而使得源码具有更加清晰的逻辑**。

### 2.1  函数装饰器

#### 函数的函数装饰器

我们还是以为函数添加计时功能为例，讲述函数装饰器。

```
import time

def decorator(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        func()
        end_time = time.time()
        print(end_time - start_time)

    return wrapper

@decorator 
def func():
    time.sleep(0.8)

func() # 函数调用
# 输出：0.800644397735595 
```

在上面代码中 func是我要装饰器的函数，我想用装饰器显示func函数运行的时间。@decorator这个语法相当于 执行 func = decorator(func)，为func函数装饰并返回。在来看一下我们的装饰器函数 - decorator，该函数的传入参数是func （被装饰函数），返回参数是内层函数。这里的内层函数-wrapper，其实就相当于闭包函数，它起到装饰给定函数的作用，wrapper参数为*args, **kwargs。*args表示的参数以列表的形式传入；**kwargs表示的参数以字典的形式传入：

　　　　　　　　![img](https://images2017.cnblogs.com/blog/1251096/201710/1251096-20171028155445320-839180786.png)

从图中我们可以看到：凡是以key=value形式的参数均存在kwargs中，剩下的所有参数都以列表的形式存于args中。这里要注意的是：为了不破坏原函数的逻辑，我们要保证内层函数wrapper和被装饰函数func的传入参数和返回值类型必须保持一致。

#### 类方法的函数装饰器

　　类方法的函数装饰器和函数的函数装饰器类似。

```
import time

def decorator(func):
    def wrapper(me_instance):
        start_time = time.time()
        func(me_instance)
        end_time = time.time()
        print(end_time - start_time)
    return wrapper

class Method(object):

    @decorator 
    def func(self):
        time.sleep(0.8)

p1 = Method()
p1.func() # 函数调用
```

对于类方法来说，都会有一个默认的参数self，它实际表示的是类的一个实例，所以在装饰器的内部函数wrapper也要传入一个参数 - me_instance就表示将类的实例p1传给wrapper，其他的用法都和函数装饰器相同。

### 2.2 类装饰器

　　前面我们提到的都是让 函数作为装饰器去装饰其他的函数或者方法，那么可不可以让 一个类发挥装饰器的作用呢？答案肯定是可以的，一切皆对象嚒，函数和类本质没有什么不一样。类的装饰器是什么样子的呢？

```
class Decorator(object):
    def __init__(self, f):
        self.f = f
    def __call__(self):
        print("decorator start")
        self.f()
        print("decorator end")

@Decorator
def func():
    print("func")

func()
```

这里有注意的是：**__call__()是一个特殊方法，它可将****一个类实例变成一个可调用对象**:

 

```
p = Decorator(func) # p是类Decorator的一个实例
p() # 实现了__call__()方法后，p可以被调用
```

要使用类装饰器必须实现类中的__call__()方法，就相当于将实例变成了一个方法。

### 2.3  装饰器链

　　一个python函数也可以被多个装饰器修饰，要是有多个装饰器时，这些装饰器的执行顺序是怎么样的呢？

　　　　　　　　![img](https://images2017.cnblogs.com/blog/1251096/201710/1251096-20171028170526992-2025082647.png)

可见，多个装饰器的执行顺序：是**从近到远**依次执行。

### 2.4  python装饰器库 - functools

```
def decorator(func):
    def inner_function():
        pass
    return inner_function

@decorator
def func():
    pass

print(func.__name__)

# 输出： inner_function
```

 上述代码最后执行的结果不是 func，而是 inner_function！这表示被装饰函数自身的信息丢失了！怎么才能避免这种问题的发生呢？

可以借助functools.wraps()函数：

```
from functools import wraps
def decorator(func):
    @wraps(func) 
    def inner_function():
        pass
    return inner_function

@decorator
def func():
    pass

print(func.__name__)

#输出： func
```