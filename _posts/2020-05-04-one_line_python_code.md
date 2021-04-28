---
layout: post
title: "What can One-Line-Python-Code do?"
description: "Life is short, so I use Python."
comments: false
keywords: "Python"
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=27733963&auto=1&height=66"></iframe>

# 开始

问：一行Python代码能干啥？

答：很多东西！

这些代码不用装pip就可以运行

我们可以在 [Python云端控制台](https://console.python.org/python-dot-org-console/) 来玩耍

<iframe src="https://console.python.org/python-dot-org-console/" style="width: 100%; height: 300px;"></iframe>

![](//panzhifei.fun/img/2020/05/04/02/p1.jpg)

# 一行代码打印心形

![](//panzhifei.fun/img/2020/05/04/02/p2.jpg)

```python
print('\n'.join([''.join([('ILOVEYOU'[(x-y) % len('ILOVEYOU')] if ((x*0.05)**2+(y*0.1)**2-1)**3-(x*0.05)**2*(y*0.1)**3 <= 0 else' ') for x in range(-30, 30)]) for y in range(30, -30, -1)]))
```

# 一行代码解决八皇后问题

![](//panzhifei.fun/img/2020/05/04/02/p3.jpg)

```python
[__import__('sys').stdout.write('\n'.join('.' * i + 'Q' + '.' * (8-i-1) for i in vec) + "\n========\n") for vec in __import__('itertools').permutations(range(8)) if 8 == len(set(vec[i]+i for i in range(8))) == len(set(vec[i]-i for i in range(8)))]
```

# 一行代码打印斐波那契数列

![](//panzhifei.fun/img/2020/05/04/02/p4.jpg)

```python
print([x[0] for x in [(a[i][0], a.append([a[i][1], a[i][0]+a[i][1]])) for a in ([[1, 1]], ) for i in range(30)]])
```
