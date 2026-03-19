---
title: python 元类
tags: 
  - python
categories: 
  - 技术
date: 2026-03-19
---
## python 元类


```python
class Car(object):
    def __init__(self,name):
        print('init')
        self.name=name
    def __new__(cls, *args, **kwargs):
        print('new')
        return super().__new__(cls)
    
obj = Car('雪佛兰')

# 输出
# new
# init
```

##### 	根据类创建对象 `obj = Car('雪佛兰')`  

1. 执⾏类的 new ⽅法， 创建空对象 【构造⽅法】   {}

2. 执⾏类的 init ⽅法，初始化对象 【初始化⽅法】 {name: "雪佛兰"}



##### 	问：对象是类创建的，类是谁创建的？

​	**答：类是由type创建。**



#### type创建类

```python
# 传统⽅式创建类
class Foo(object):
    v1 = 123
 	def func(self):
 		return 666
    
# ⾮传统⽅式创建类
Fa = type("Foo", (object,),{"v1": 123, "func":lambda self:666})
# 1 创建类 
# 参数        - 类名 - 继承类 - 成员
# 2 根据类创建对象
obj = Fa()
# 3 调⽤对象中的v1变量
print(obj.v1)
# 4 执⾏对象中的func⽅法
result = obj.func()
```



#### metaclass 元类

```python
class MyType(type):
    pass
class Foo(object, metaclass=MyType):
    pass
# Foo类由MyType创建
```



```python
class MyType(type):
    def __init__(self, *args, **kwargs):
        print('init')
        super().__init__(*args, **kwargs)

    def __new__(cls, *args, **kwargs):
        print('new')
        return super().__new__(cls, *args, **kwargs)

    def __call__(self, *args, **kwargs):
        print('call')
        # 调⽤⾃⼰的那个类 __new__ ⽅法去创建对象
        empty_object = self.__new__(self)
        # 调⽤你⾃⼰的 __init__ ⽅法取初始化
        self.__init__(empty_object, *args, **kwargs)
        return empty_object

class Foo(object, metaclass=MyType):
    def __init__(self, name):
        print('foo init')
        self.name = name

    def __new__(cls, *args, **kwargs):
        print('foo new')
        return super().__new__(cls, *args, **kwargs)
obj = Foo('ifan')

## class Foo(object, metaclass=MyType):
#      ....
#   执行到这一步 会调用 type的 call方法 在call方法中先调用 类的 new，在调用 类的 init
#  class Foo():... => type call() =>  mytype new()  => mytype init()
#  输出 new init


## obj = Foo('ifan')
#  obj对象 由Foo类创建，Foo类（对象）由Mytype类创建
#  调用 Foo('ifan')  => Mytype call() => Foo new() => Foo init()
#  输出 call   foo new    foo init


## obj() =>  Foo call()
```



#### 元类创建 单例模式 

```python
class myType(type):
    def __init__(self, *args, **kwargs):
        super().__init__( *args, **kwargs)
        self.instance=None
        
    def __new__(cls, *args, **kwargs):
        return super().__new__(cls, *args, **kwargs)
    
    def __call__(self, *args, **kwargs):
        if not self.instance:
            self.instance = self.__new__(self)
        self.__init__(self.instance, *args, **kwargs)
        return self.instance

class per(metaclass=myType):
    pass
a = per()
b = per()
print(a,b)

```

