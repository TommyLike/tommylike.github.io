---
layout: post
title:  "Python常见特性入门"
subtitle:   "Python常见的特性入门"
date:   2016-08-14 21:59:44 +0800
categories: python
author: "tommylike"
header-img: "img/posts/telephone.jpg"
catalog: true
tags:
    - python

---

# Python常见特性入门

## 装饰器
有过AOP编程经历的人对以下的场景肯定都不陌生:我们暴露了API接口给客户端调用，基于运维的考虑，我们需要自动拦截API接口的耗时参数等信息，通常的方式就是在基类中包装一层或者使用拦截器，大致的代码如下:  
```csharp
public string WrapExecute(string fake_param)
{
  ExecuteBefore(fake_param);
  var result = Execute();
  ExecuteAfter(result);
  return result
}
```
Python的装饰器天生就可以承担类似的工作,下面是一个简单的装饰器:  
```python
def execute_before():
    print('this is before')


def execute_after():
    print('this is after')


def decorator(func):

    def wrapper():
        execute_before()
        func()
        execute_after()

    return wrapper


def execute():
    print('this is executing')

execute = decorator(execute)
```
跟我们在其他语言中的用法保持一致，当然我们的python在此之上，还提供了更便捷的方式:**@**,python中以@开头并紧跟装饰器的名字可理解成给对应的对应的对象使用装饰器，所以，上面的调用方式，可以优化成:
```python
@decorator
def execute():
    pass
```
通常情况下，被修饰的函数都是带有参数的，为了能在装饰器中获取参数信息，python中引入了可变参数的概念，我们把我们的wrapper函数调整为如下:
```python
de decorator(func)

  def wrapper(*args, **kwargs)
  execute_before()
  func(args, kwargs)
  execute_after()
#other code
```
还有一种情况，就是我们的装饰器本身是可以支持配置参数的，在这种情况下，我们往往还需要在外面再增加一层，在现在的例子基础上，比如我们需要支持配置日志级别,那代码可调整如下:
```python
def outter_wrapper(log_level='info')
  def decorator(func):

      def wrapper():
          execute_before(log_level)
          func()
          execute_after(log_level)
      return wrapper

  return decorator

@outter_wrapper(log_level='error')
def execute():
  pass
```
## 函数式编程

## 可变长度的参数

## 生成器

## 迭代器

## 原类

## 描述器(Descriptor)

## 协程
