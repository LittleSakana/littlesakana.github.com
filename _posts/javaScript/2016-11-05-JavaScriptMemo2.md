---
layout: article
title: "JavaScript Memo (二)"
categories: javaScript
excerpt: "基本语法中的条件判断和循环"
ads: true
share: false
image:
---

> 基本语法中的条件判断和循环。

### 条件判断if-else

>不解释，只有一点注意，JavaScript把null、undefined、0、NaN和空字符串''视为false，其他值一概视为true

```
var age = 3;
if (age >= 18) {
    alert('adult');
} else if (age >= 6) {
    alert('teenager');
} else {
    alert('kid');
}
```

### for循环

>for循环最常用的地方是利用索引来遍历数组

```
var arr = ['Apple', 'Google', 'Microsoft'];
var i, x;
for (i=0; i<arr.length; i++) {
    x = arr[i];
    alert(x);
}
```
>for循环的一个变体是for ... in循环，它可以把一个对象的所有属性依次循环出来

```
var o = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};
for (var key in o) {
    alert(key); // 'name', 'age', 'city'
}
```

### for ... in

>for ... in循环由于历史遗留问题，它遍历的实际上是对象的属性名称,一个Array数组实际上也是一个对象，它的每个元素的索引被视为一个属性

```
var a = ['A', 'B', 'C'];
a.name = 'Hello';
for (var x in a) {
    alert(x); // '0', '1', '2', 'name'
}
```

### for ... of

>遍历Array可以采用下标循环，遍历Map和Set就无法使用下标。为了统一集合类型，ES6标准引入了新的iterable类型，Array、Map和Set都属于iterable类型
>
>具有iterable类型的集合可以通过新的for ... of循环来遍历

```
var a = ['A', 'B', 'C'];
var s = new Set(['A', 'B', 'C']);
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
for (var x of a) { // 遍历Array
    alert(x);// 'A', 'B', 'C'
}
for (var x of s) { // 遍历Set
    alert(x);
}
for (var x of m) { // 遍历Map
    alert(x[0] + '=' + x[1]);
}
```

### forEach()

>ES5.1标准引入forEach()方法
>
>它接收一个函数，每次迭代就自动回调该函数

```
var a = ['A', 'B', 'C'];
a.forEach(function (element, index, array) {
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    alert(element);
});

var s = new Set(['A', 'B', 'C']);
s.forEach(function (element, sameElement, set) {
    alert(element);
});

var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
m.forEach(function (value, key, map) {
    alert(value);
});
```