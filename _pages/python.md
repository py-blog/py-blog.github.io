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
```python
# str-tools.py

class StrTools:
    pass

str_tool = StrTools()

# Singleton
from str_tools import str_tool

s1 = str_tool
s2 = str_tool

print(id(s1))
print(id(s2))
```
```python
# Factory Pattern

class Person:
    pass
class Worker(Person):
    print('Worker')
class Student(Person) :
    print('Student')
class Teacher(Person):
    print('Teacher')

class Factory:
    def get_person(self, p_type):
        if p_type == 'w':
            return Worker()
        elif p_type == 's':
            return Student()
        else:
            return Teacher()

factory = Factory()
worker = factory.get_person('w')
stu = factory.get_person('s')
teacher = factory.get_person('t')
```
```python
import time
import threading

def sing():
    while True:
        print('sing...')
        time.sleep(1)

def dance():
    while True:
        print('dance...')
        time.sleep(1)

if __name__ == '__main__':
    sing_thread = threading.Thread(target=sing)
    dance_thread = threading.Thread(target=dance)

    sing_thread.start()
    dance_thread.start()
```
```python
# Socket服务器端开发
# https://github.com/nicedayzhu/netAssist/releases

import socket
# 创建Socket对象
socket_server = socket.socket()
# 绑定ip地址和燃口
socket_server.bind(("localhost", 8888))
# 监听端口
socket_server.listen(1)
# listen方法内接受一个整数传参数,表示接受的链接数量
# 等待客户端链接
# result: tuple = socket_server .accept()
# conn = result[0]     # 客户端和服务端的链接对象
# address = result[1]  # 客户端的地址信息
conn,address = socket_server.accept()
# accept方法返回的是二元元组(链接对象，客户端地址信息)
# 可以通过变量1，变量2 = socket_server.accept()的形式，直接接受二元元组内的两个元素
# accept()方法，是阻塞的方法，等待客户端的链接，如果没有链接，就卡在这一行不向下执行了

print(f"接收到了客户端的链接，客户端的信息是:{address}")

# 接受客户端信息，要使用客户端和服务端的本次链接对象，而非socket_server对象
data: str = conn.recv(1024).decode("UTF-8")
# recv接受的参数是缓冲区大小,一般给1024即可
# recv方法的返回值是一个字节数组也就是bytes对象，不是字符串，可以通过decode方法通过UTF-8编码，将字节数组转换为字符串对象
print(f"客户端发来的消息是: {data}" )
# 发送回复消息
msg = input("请输入你要和客户端回复的消息。").encode("UTF-8") # encode可以将字符串编码为字节数组对象
conn.send(msg)
# 关闭链接
conn.close()
socket_server.close()
```
```python
"""
Socket客户端开发
"""
import socket
# 创建socket对象
socket_client = socket.socket()
# 连接到服务端
socket_client.connect(("localhost", 8888))

while True:
    # 发送消息
    msg = input("请输入要给服务端发送的消.息:")
    if msg == 'exit':
        break
    socket_client.send(msg.encode( "UTF-8"))
    #接收返回消息
    recv_data = socket_client.recv(1024)   #1024是缓冲区的大小，一般1024即可。同样recv方法是阻塞的
    print(f"服务端回复的消息是:{recv_data.decode(' UTF-8')}")
# 关闭链接
socket_client.close()
```
```python
# recursion

import os

def get_files_recursion_from_dir(path):
    file_list = []
    if os.path.exists(path):
        for f in os.listdir(path):
            new_path = path + "/" + f
            if os.path.isdir(new_path):
                file_list += get_files_recursion_from_dir(new_path)
            else:
                file_list.append(new_path)
    else:
        print(f"指定的目录{path}，不存在")
        return []

    return file_list

if __name__ == '__main__':
    print(get_files_recursion_from_dir("E:\test"))
```
```python
# polymorphism

class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(se1f):
        print("汪汪汪")

class Cat(Animal):
    def speak(se1f):
        print("喵喵喵")

def make_noise(animal:Animal):
    animal.speak()

dog = Dog()
cat = Cat()

make_noise(dog)
make_noise(cat)
```
