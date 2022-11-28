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
