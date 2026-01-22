---
title: CS61A高阶函数笔记
date: 2026-01-22 20:52:43
tags:
---
    果然在学习cs61a前请先学习一部分python语法，毕竟这门课程叫sicp而非python语法入门哦
    本文建立在学习过简单C和python语法的前提下
## 函数互相调用
函数可以调用其他函数，

在C语言里我经常用``while(scanf("%d", &x) != 1)``来检测输入字符是否为数字，这里就同时用到了while()函数和scanf()函数。类似的，python也可以在函数里调用另一个函数，如：
```
def summation(n, term):
	    total, k = 0, 1
	    while k <= n:
	        total, k = total + term(k), k + 1
	    return total
	
	def cube(x):
	    return x*x*x
	
	def sum_cubes(n):
	    return summation(n, cube)

	result = sum_cubes(3)
```
为了计算 1 到 n 的自然数的立方之和，教材将循环与立方结合起来（python可以自动检测类型这一点特别方便，再也不用担心double和int冲突了）

读到这我想问 return summation(n, cube) 这一步不需要指定cube(n)吗？
    
    Gemini：不需要，而且"不能"
我们需要summation用cube函数明白我们需要给每个数乘立方，如果输入cube(n)会返回一个已经计算好的n³，python反而就不会算了。

    Gemini：
    我们可以把这个逻辑类比为“雇佣厨师”的过程：
    summation 是一个厨师，他知道如何处理一系列原材料(k=1 到 n)，但他不知道具体要做什么菜。
    cube 是一张“立方菜谱”。
    当你执行 summation(n, cube) 时，你是在告诉厨师：“请按照这张菜谱，把这 n 个材料依次处理一遍。”厨师拿到菜谱后，会在需要的时候（循环中）去查看菜谱并操作。
    如果你给的是 cube(n)，就相当于你直接给了厨师一个“已经做好的菜（比如一盘糖醋里脊）”。厨师不知道怎么用这一盘菜去处理剩下的原材料，逻辑就卡住了。


## 嵌套定义
```
def compose1(f, g):
    def h(x):
        return f(g(x))
    return h
```
这样我们就可以compose1(a, b)来调用a(b(x))了

### a(x)(y)高阶函数是什么？
这个cs61a课本太高大上了，这里用一种简单的例子：
```
def adder(x):
   def inner(y):
       return x + y
   return inner
add_five = adder(5)
print(add_five(10)) # 输出: 15
```
这里的`add_five(10)`可以写成`adder(5)(10)`。我的解释如下：
函数里套了另一个函数，如`adder(5)(10)`可以看成
```
def inner(10):
    x = 5
    return x+y
adder返回inner，也就是15
```
按教材的说法这个似乎叫柯里化

## lembda
就当成一个简单的def好咯，比如x²
``s = lambda x: x * x``

## 牛顿法
这一部分建议一边看[OIWIKI](https://oi-wiki.org/math/numerical/newton/)一边理解

eps指一个很小的整数，其实就是微积分里的$\epsilon$
