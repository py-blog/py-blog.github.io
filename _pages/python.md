---
title: Python语法
author: Zhang
date: 2022-08-08
category: code
layout: post
---

```python
# Python装饰器本质上是对函数闭包的语法糖

import time

def count_time_wrapper(func):
    """
    闭包,用于增强函数func: 给函数func增加统计时间的功能
    """

    def improved_func():
        start_time = time.clock() 	# 起始时间
        func()  					# 执行函数
        end_time = time.clock()  	# 结束时间
        print("it takes {} s to find all the olds".format(end_time - start_time))

    return improved_func


@count_time_wrapper
def print_odds():
    """
    输出0~100之间所有奇数,并统计函数执行时间
    """
    for i in range(100):
        if i % 2 == 1:
            print(i)


if __name__ == '__main__':
    # 装饰器等价于在第一次调用函数时执行以下语句:
    # print_odds = count_time_wrapper(print_odds)
    print_odds()
```
```python
list(map(lambda x:x*x,[1,2,3]))
```
```python
# nonlocal 在函数外部得到函数内的局部变量
def outer_fun(initial_amount=0):

    def inner_fun(num,deposit=True):
        nonlocal initial_amount
        if deposit:
            initial_amount += num
            print(f"存款： + {num},余额：{initial_amount}")
        else:
            initial_amount -= num
            print(f"取款： - {num},余额：{initial_amount}")
    
    return inner_fun

atm = outer_fun()

atm(10)
```
