---
title: ES6
date: 2024-10-19 10:56:32
tags:
---
# ES6

### 1. let 和 const 命令
- let 
    - 无变量提升，是一个块级作用域，不能重复声明
- const 
    - 无变量提升，是一个块级作用域，不能重复声明
    - 声明常量，一旦声明，不能修改值
    - 声明对象时，不能直接修改对象，但是可以修改对象的属性值
- 建议：在默认情况下使用const，只有在需要修改变量时才使用let。


### 2.模板字符串
- ![模板字符串](/images/ES6-str.png)

### 3.强大函数

- 默认值
![默认值](/images/ES6-f1.png)

- 默认值可以是函数
![默认值函数](/images/ES6-f2.png)

- 剩余参数：使用...keys参数，可以获取函数中余下的参数
![剩余参数](/images/ES6-f3.png)

- 扩展运算符：将一个数组进行分割，并将各个项作为分离参数传给函数
![扩展运算符](/images/ES6-f4.png)

- 箭头函数：(=>)可以简化函数定义，并且不绑定this，可以用作回调函数
![箭头函数](/images/ES6-f5.png)

### 4.解构赋值

- 对赋值运算符的一种扩展
![解构赋值](/images/ES6-jg1.png)

![解构赋值](/images/ES6-jg2.png)

### 5.扩展对象功能

- ![扩展对象功能](/images/ES6-obj1.png)

- ![扩展对象功能](/images/ES6-obj2.png)

### 6.Symbol对象

- 一种新的原始数据类型，是通过Symbol函数生成的
- 它是一种独一无二的值，可以作为对象属性的标识符，可以保证对象属性的私密性
- 最大用途，定义对象的私有变量

- ![Symbol对象](/images/ES6-sy1.png)

- ![获取Symbol声明的属性名](/images/ES6-sy2.png)

### 7.Set数据结构

- Set：类似数组，但是成员的值都是唯一的，没有重复的值
- Map：类似对象，是一对键值对的集合，类似于哈希表
- ![Set](/images/ES6-set1.png)
- ![Set转化为数组](/images/ES6-set2.png)

### 8.Map数据结构

- Map：类似对象，是一对键值对的集合，类似于哈希表
- ![Map](/images/ES6-map1.png)

### 9.数组的扩展

- from()：将类数组对象转换为数组
- of()：将一组值转换为数组
- copyWithin()：浅复制数组的一部分到同一数组中的另一个位置
- find()：返回数组中满足条件的第一个元素
- findIndex()：返回数组中满足条件的第一个元素的索引
- keys，values，entries()：返回数组的键名，键值，键值对
- ![数组的扩展](/images/ES6-arr1.png)
- ![数组的扩展](/images/ES6-arr2.png)
- ![数组的扩展](/images/ES6-arr3.png)
- ![数组的扩展](/images/ES6-arr4.png)
- ![数组的扩展](/images/ES6-arr5.png)

### 10.迭代器

- 一种接口，用来访问集合对象的元素，通过Symbol.iterator属性来访问，通过next()方法来获取下一个元素
- 用于遍历数组结构的指针
- ![迭代器](/images/ES6-dd1.png)


### 11.生成器

- 一种特殊的函数，使用yield关键字来挂起函数
- 为了改变执行流程，可以暂停函数的执行，并恢复函数的执行
- 一般用于异步编程
- ![生成器](/images/ES6-yield1.png)
- ![生成器](/images/ES6-yield2.png)

### 12.Promise对象

- 相当于一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果
- 各种异步操作都可以用同样的方法进行处理
- 特点：
    - 对象的状态不受外界影响：pending（进行中），fulfilled（已成功），rejected（已失败）
    - 一旦状态改变，就不会再变，任何时候都可以得到这个结果

### 13.async/await

- 异步编程的终极解决方案
- async会返回一个Promise对象，是Generator函数的语法糖
- await关键字后面可以跟Promise对象，表示等待Promise对象的状态变为resolved，然后才会继续执行后面的语句
- 异步函数返回的是Promise对象，可以使用then()方法添加回调函数
- ![async/await](/images/ES6-async1.png)

### 14.Class

- ES6中引入的新语法，用来定义类
- 类可以用来创建自定义的构造函数，实例属性和方法
- 类可以继承其他类，可以实现多态
- 类可以实现接口，可以对类的实例进行类型检查
- ![Class](/images/ES6-class1.png)

- 继承：extends关键字后面可以跟父类，子类会自动获得父类的属性和方法
- ![继承](/images/ES6-class2.png)
- ![继承](/images/ES6-class3.png)

### 15.模块化

- 模块化是指将一个大程序分解成小的、可管理的、可复用的模块
- ES6模块化方案，主要有以下几种：
    - CommonJS：模块化规范，主要用于服务器端
    - AMD：异步模块定义，主要用于浏览器端
    - UMD：通用模块定义，同时支持AMD和CommonJS
    - ES6模块：模块化方案，主要用于浏览器端和Node.js
    - export：用于导出模块成员
    - import：用于导入模块成员