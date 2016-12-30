---
layout: article
title: "JavaScript Memo (一)"
categories: javaScript
excerpt: "1995年，网景公司的Brendan Eich在两周之内设计出了JavaScript语言"
ads: true
share: false
image:
---

## 简介

**JavaScript是一种运行在浏览器中的解释型的编程语言。**
>1995年，网景公司的Brendan Eich在两周之内设计出了JavaScript语言。

#### ECMAScript

>因为网景开发了JavaScript，一年后微软又模仿JavaScript开发了JScript，为了让JavaScript成为全球标准，几个公司联合ECMA（European Computer Manufacturers Association）组织定制了JavaScript语言的标准，被称为ECMAScript标准。

>ECMAScript是一种语言标准，而JavaScript是网景公司对ECMAScript标准的一种实现。

>最新版ECMAScript 6标准（简称ES6）已经在2015年6月正式发布了，所以，讲到JavaScript的版本，实际上就是说它实现了ECMAScript标准的哪个版本。

## 基本语法

* 语句以;结束
* 语句块用{...}
* 以//开头直到行末的字符被视为行注释
* 块注释是用/\*...*/把多行字符包裹起来

### 数据类型

### Number

>JavaScript不区分整数和浮点数，统一用Number表示，以下都是合法的Number类型

```
123; // 整数123
0.456; // 浮点数0.456
1.2345e3; // 科学计数法表示1.2345x1000，等同于1234.5
-99; // 负数
NaN; // NaN表示Not a Number，当无法计算结果时用NaN表示
Infinity; // Infinity表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示为Infinity
```
>Number四则运算

```
1 + 2; // 3
(1 + 2) * 5 / 2; // 7.5
2 / 0; // Infinity
0 / 0; // NaN
10 % 3; // 1
10.5 % 3; // 1.5
```

### 字符串

>字符串是以单引号'或双引号"括起来的任意文本，比如'abc'，"xyz"等等。
>
>转义字符\可以转义很多字符，\n表示换行，\t表示制表符，字符\本身也要转义，\\\表示的字符就是\
>
>ASCII字符可以以\x##形式的十六进制表示`'\x41'; // 完全等同于 'A'`
>
>用\u####表示一个Unicode字符`'\u4e2d\u6587'; // 完全等同于 '中文'`

>多行字符串，ES6新增用\` ... `表示

```
`这是一个
多行
字符串`;
```
>用+号连接字符串,ES6新增了一种模板字符串

```
var name = '小明';
var age = 20;
var message = '你好, ' + name + ', 你今年' + age + '岁了!';
alert(message);

ES6新模板字符串
var message = `你好, ${name}, 你今年${age}岁了!`;
alert(message);
```
>获取字符串某个指定位置的字符，使用类似Array的下标操作，索引号从0开始

```
var s = 'Hello, world!';

s[0]; // 'H'
s[6]; // ' '
s[7]; // 'w'
s[12]; // '!'
s[13]; // undefined 超出范围的索引不会报错，但一律返回undefined
```
**注意：字符串是不可变的，如果对字符串的某个索引赋值，不会有任何错误，但是，也没有任何效果**

**JavaScript为字符串提供了一些常用方法，调用这些方法本身不会改变原有字符串的内容，而是返回一个新字符串**

### 布尔值

>一个布尔值只有true、false两种值，要么是true，要么是false

```
true; // 这是一个true值
false; // 这是一个false值
2 > 1; // 这是一个true值
2 >= 3; // 这是一个false值
```
***注意：JavaScript允许对任意数据类型做比较***

**要特别注意相等运算符==。JavaScript在设计时，有两种比较运算符：**

**第一种是==比较，它会自动转换数据类型再比较，很多时候，会得到非常诡异的结果；**

**第二种是===比较，它不会自动转换数据类型，如果数据类型不一致，返回false，如果一致，再比较。**

**由于JavaScript这个设计缺陷，不要使用==比较，始终坚持使用===比较。**

**另一个例外是NaN这个特殊的Number与所有其他值都不相等，包括它自己`NaN === NaN; // false`**

### 数组

>JavaScript的数组可以包括任意数据类型

```
[1, 2, 3.14, 'Hello', null, true];
new Array(1, 2, 3);
```
>**注意，直接给Array的length赋一个新的值会导致Array大小的变化**

```
var arr = [1, 2, 3];
arr.length; // 3
arr.length = 6;
arr; // arr变为[1, 2, 3, undefined, undefined, undefined]
arr.length = 2;
arr; // arr变为[1, 2]
```
>Array通过indexOf()来搜索一个指定的元素的位置
>slice()截取Array的部分元素，然后返回一个新的Array

```
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']
```
>push()向Array的末尾添加若干元素，pop()则把Array的最后一个元素删除掉
>
>unshift()方法往Array的头部添加若干元素，shift()方法把Array的第一个元素删掉
>
>sort()对当前Array进行排序
>
>reverse()把整个Array反转
>
>splice()方法修改Array，从指定的索引开始删除若干元素，然后再从该位置添加若干元素

```
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```
>concat()方法把当前的Array和另一个Array连接起来，并返回一个新的Array，它可以接收任意个元素和Array，并且自动把Array拆开，然后全部添加到新的Array里
>join()方法把当前Array的每个元素都用指定的字符串连接起来，然后返回连接后的字符串

```
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); // 'A-B-C-1-2-3'
```


### 对象

>JavaScript的对象是一组由键-值组成的无序集合,键都是字符串类型，值可以是任意数据类型。

```
var person = {
    name: 'Bob',
    age: 20,
    tags: ['js', 'web', 'mobile'],
    city: 'Beijing',
    hasCar: true,
    zipcode: null
};
```
>JavaScript的对象是动态类型，你可以自由地给一个对象添加或删除属性

```
var xiaoming = {
    name: '小明'
};
xiaoming.age; // undefined
xiaoming.age = 18; // 新增一个age属性
xiaoming.age; // 18
delete xiaoming.age; // 删除age属性
xiaoming.age; // undefined
delete xiaoming['name']; // 删除name属性
xiaoming.name; // undefined
delete xiaoming.school; // 删除一个不存在的school属性也不会报错
```
>如果要检测对象是否拥有某一属性，包括继承得到的，可以用in操作符
>要判断一个属性是否是自身拥有的，而不是继承得到的，可以用hasOwnProperty()方法

```
var xiaoming = {
    name: '小明'
};
'name' in xiaoming; // true
'toString' in xiaoming; // true
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false
```

### Map

>JavaScript的对象有个问题，就是键必须是字符串。但实际上Number或者其他数据类型作为键也是合理的。为了解决这个问题，最新的ES6规范引入了新的数据类型Map。
>
>Map是一组键值对的结构，具有极快的查找速度。

```
var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.set('Bob', 59);
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam'
m.get('Adam'); // undefined
```

### Set

>Set也是一组key的集合，但不存储value。由于key不能重复，所以，在Set中，没有重复的key。
>
>重复元素在Set中自动被过滤
>
>通过add(key)方法添加元素到Set中
>
>通过delete(key)方法删除元素

```
var s = new Set([1, 2, 3, 3, '3']);
s; // Set {1, 2, 3, "3"}
s.add(4);// 添加元素4
s.delete(3);// 添加元素3
```

### 变量

**变量本身类型不固定的语言称之为动态语言，与之对应的是静态语言。静态语言在定义变量时必须指定变量类型，如果赋值的时候类型不匹配，就会报错。**

```
var a; // 申明了变量a，此时a的值为undefined
var $b = 1; // 申明了变量$b，同时给$b赋值，此时$b的值为1
var s_007 = '007'; // s_007是一个字符串
var Answer = true; // Answer是一个布尔值true
var t = null; // t的值是null
```