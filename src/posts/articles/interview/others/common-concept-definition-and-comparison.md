---
view: post
layout: post
lang: zh-cn
author: realign
title: 常见概念定义以及对比
description: 常见概念定义以及对比
excerpt: 常见概念定义以及对比
cover: true
coverConfig:
  - type: js
  - iconType: js
  - title: Javascript
  - subTitle: X ? Y ? Z
categories:
  - api
  - js
  - css
tags:
  - api
  - js
  - css
created_at: 2020-04-02 14:43
updated_at: 2020-04-02 16:41
meta:
  - name: keywords
    content: js, css, api, 常见概念, 概念对比
---

## call-apply-bind

> Function

一句话：都是为了改变某个函数运行时的上下文（context）而存在的。

### call-apply-bind 签名

```js
function.call(thisArg, arg1, arg2, ...)
function.apply(thisArg, [argsArray])
function.bind(thisArg[, arg1[, arg2[, ...]]])
```

### call-apply-bind 相似点

1. 都是用来改变函数体 `this` 的指向
2. 第一个参数都是 `this` 要指向的对象
3. 都可以利用后续参数传参

### call-apply-bind 不同点

一个通用的例子：

```js
var X = {
  name: 'xxx',
  gender: 'male',
  age: 18,
  say() {
    console.log(`${this.name}, ${this.gender}, ${this.age} years old.`);
  },
};
```

对于 `X` 的 `say` 方法，执行接入如下：

```js
X.say(); // xxx, male, 18 years old.
```

现在有个 `Y`，定义如下：

```js
var Y = {
  name: 'yyy',
  gender: 'female',
  age: 16,
};
```

那，如何复用 `X` 的 `say` 方法来显示 `Y` 的数据呢？

```js
// call
X.say.call(Y); // yyy, female, 16 years old.

// apply
X.say.apply(Y); // yyy, female, 16 years old.

// bind
X.say.bind(Y)(); // yyy, female, 16 years old.

// bind
X.say.bind(Y); //
```

直接写 `X.say.bind(Y)` 是不会有任何结果的！！！

看到区别了吗？

- `call` 和 `apply` 都是对函数的直接调用
- `bind` 返回的仍然是一个函数，需要显式调用

把通用例子稍改写一下：

```js
var X = {
  name: 'xxx',
  gender: 'male',
  age: 18,
  say(food, sport) {
    console.log(`${this.name}, ${this.gender}, ${this.age} years old.
Like to eat ${food} and ${sport}.`);
  },
};
```

同样，`Y` 复用 `X` 的 `say` 方法：

```js
// call
X.say.call(Y, 'noodles', 'running');
// yyy, female, 16 years old.
// Like to eat noodles and running.

// apply
X.say.apply(Y, ['noodles', 'running']);
// yyy, female, 16 years old.
// Like to eat noodles and running.

// bind
X.say.bind(Y)('noodles', 'running');
// yyy, female, 16 years old.
// Like to eat noodles and running.
```

例子很清楚了，`call` 和 `apply` 的区别也就有了：

- `call` 的非第一个参数，与 `say` 方法的参数是一一对应的
- `apply` 的第二个参数是一个数组，数组的元素是和 `say` 方法中一一对应的
- `bind`返回的是一个函数，正常函数传参即可

## slice-substr-substring

> String

一句话：都是截取字符串。

### slice-substr-substring 签名

```js
// 从一个字符串中提取字符串并返回新字符串
// 参数可为负数。第二个参数是指定结束位置
str.slice(beginIndex[, endIndex])

// 返回一个字符串中从指定位置开始到指定字符数的字符
// 参数可为负数。第二个参数是指定截取长度
str.substr(start[, length])

// 返回一个字符串在开始索引到结束索引之间的一个子集, 或从开始索引直到字符串的末尾的一个子集
// 参数为负数被替换成 0；【内部保证非负】
// indexStart < indexEnd；【内部保证小参在前】，会强制被换掉
str.substring(indexStart[, indexEnd])
```

### slice-substr-substring 从效果看差异

```js
var str = 'helloworld!';

str.substr(2, 5); // 'llowo'
str.slice(2, 5); // 'llo'
str.substring(2, 5); // 'llo'
```

### slice-substr-substring 相似点

[略]

### slice-substr-substring 不同点

[略]

<!-- ## call-apply-bind

> Function

一句话：都是为了改变某个函数运行时的上下文（context）而存在的。

### call-apply-bind签名

```js
function.call(thisArg, arg1, arg2, ...)
```

### call-apply-bind相似点

1. 都是用来改变函数体 `this` 的指向

### call-apply-bind不同点 -->
