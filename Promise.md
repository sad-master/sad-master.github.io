---
title: Promise
date: 2024-10-21 10:20:31
tags:
---
#   Promise

### 1.Promise 基础使用
- promise 是一个构造函数
- 其中接收一个参数 exexcutor 执行器函数，达到预期结果后，调用 resolve 函数，将结果传递给 promise；如果出现错误，调用 reject 函数，将错误信息传递给 promise。
- .then() 方法用于处理 promise 成功/失败的结果，
- .catch() 方法用于处理 promise 失败的结果。
- 组合写法：.then()成功；.catch()失败。
- ![promise基础](/images/Promise-1.1.png)
- ![promise基础](/images/Promise-1.2.png)

### 2.Promise 三个状态
- pending（等待）：初始状态，既没有被执行也没有被拒绝。
- fulfilled（已完成）：promise 成功执行，并返回一个值。
- rejected（已拒绝）：promise 执行失败，并抛出一个错误。
- 仅两种转化状态：
- 1.pending -> fulfilled：调用 resolve 函数，将结果传递给 promise。
- 2.pending -> rejected：调用 reject 函数，将错误信息传递给 promise。

### 3.Promise 的结果
- resolve 函数中可以传递成功获取的结果，.then() 方法中可以接收成功的结果。
- reject 函数中可以传递失败的原因，.catch() 方法中可以接收失败的原因。
- 注意：如果 promise 已经处于 fulfilled 或 rejected 状态，再调用 resolve 或 reject 不会起作用，而是会被忽略。

### 4.Promise封装ajax
- ![promise封装ajax](/images/Promise-4.1.png)
- ![promise封装ajax](/images/Promise-4.2.png)

### 5.Promise.resolve()
- 将一个普通对象或值转换成一个 Promise 对象，状态为 fulfilled。
- 如果参数是一个 Promise 对象，则直接返回该对象。
- 用途：设置缓存结构，减小后端压力

### 6.Promise.reject()
- 将一个普通对象或值转换成一个 Promise 对象，状态为 rejected。
- 如果参数是一个 Promise 对象，则直接返回该对象。
- 用途：对于成功的promise对象中的个例进行错误处理

### 7.Promise链式调用
- .then()返回的新 promise 对象，可以继续调用 .then() 方法。
- 不执行return，则返回undefined,fulfilled状态的
- 执行return Promise.resolve(value)，则返回value,fulfilled状态的
- 执行return Promise.reject(reason)，则返回reason,rejected状态的

### 8.Promise.all()
- 用于将多个 Promise 实例，包装成一个新的 Promise 实例。
- 只有当所有 Promise 实例都成功，才会成功，否则失败。
- 成功时返回一个数组，对应每个 Promise 实例的返回值。
- 失败时返回第一个失败的 Promise 实例的错误信息。

### 9.Promise.race()
- 用于将多个 Promise 实例，包装成一个新的 Promise 实例。
- 其中一个实例率先改变状态，则新的 Promise 实例也会改变状态。
- 用途：超时判定

### 10.Promise.allSettled()
- 用于将多个 Promise 实例，包装成一个新的 Promise 实例。
- 无论 Promise 实例是成功还是失败，都会在.then()中接收到相应的结果。

### 11.Promise.any()
- 用于将多个 Promise 实例，包装成一个新的 Promise 实例。
- 只有当所有 Promise 实例都失败，才会失败，否则成功。   
- 用途：多平台的授权登录，只要有一个平台授权成功，则登录成功。

### 12.finally()
- 用于指定不管 Promise 实例是成功还是失败，都会执行的操作。
- 无论 Promise 实例是成功还是失败，都会执行指定的操作。
- 是一种特殊的透明状态，后面接.then()或.catch()方法，接收的值是之前return的值。

### 13.Async/Await
- 异步编程的语法糖，可以让异步操作变得更加方便。
- 异步函数返回一个 Promise 对象，可以使用 await 关键字获取该 Promise 对象的值。
- 异步函数中使用 await 关键字，等同于将该函数暂停，等待 Promise 对象状态改变，再恢复执行。
-  try...catch 结构，可以捕获异常。
-  ![async/await](/images/Promise-13.1.png)
