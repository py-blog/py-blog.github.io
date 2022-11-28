---
title: 正则表达式
author: Zhang
date: 2022-08-08
category: code
layout: post
---
```python
# 正则得到后缀
def getSuffix(file_name):
    return re.findall(r'.[^./:*?"<>|]+$', file_name)
    
```
```python
import re

#r1=r"^\w+[-_.]*[a-zA-Z0-9]+@[a-zA-Z0-9]+\.[a-zA-Z]{2,3}$" 
r1=r"\w+[-_.]*[a-zA-Z0-9]+@[a-zA-Z0-9]+\.[a-zA-Z]{2,3}" 
r2=r"1[3578]\d{9}"

#s1="py-code@outlook.com"
s1="py-code@outlook.com py-code666@outlook.com py-code888@outlook.com"
s2="17602108975,13726889999"

t1=re.findall(r1,s1)
t2=re.findall(r2,s2)

print (t1)
print (t2)
```
