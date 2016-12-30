---
layout: article
title: "JavaScript Memo (三)"
categories: javaScript
excerpt: "现在让我们看看函数和方法"
ads: true
share: false
image:
---

> 现在让我们看看函数和方法。

## 函数

### 定义函数

JavaScript的函数也是一个对象，下面定义的abs()函数实际上是一个函数对象，而函数名abs可以视为指向该函数的变量

```
function abs(x) {
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
}
function指出这是一个函数定义;
abs是函数的名称;
(x)括号内列出函数的参数，多个参数以,分隔;
{ ... }之间的代码是函数体，可以包含若干语句，甚至可以没有任何语句
```

### 调用函数

JavaScript允许传入任意个参数而不影响调用，因此传入的参数比定义的参数多也没有问题，虽然函数内部并不需要这些参数

```
abs(10, 'blablabla'); // 返回10
abs(-9, 'haha', 'hehe', null); // 返回9
abs(); // 返回NaN
```

arguments，它只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数,利用arguments，你可以获得调用者传入的所有参数

```
function abs() {
    if (arguments.length === 0) {
        return 0;
    }
    var x = arguments[0];
    return x >= 0 ? x : -x;
}

abs(); // 0
abs(10); // 10
abs(-9); // 9
```

### 变量作用域

* 如果一个变量在函数体内部申明，则该变量的作用域为整个函数体，在函数体外不可引用该变量
* JavaScript的函数可以嵌套，此时，内部函数可以访问外部函数定义的变量

```
'use strict';

function foo() {
    var x = 1;
    function bar() {
        var x = 'A';
        alert('x in bar() = ' + x); // 'A'
    }
    alert('x in foo() = ' + x); // 1
    bar();
}
```
JavaScript的函数定义有个特点，它会先扫描整个函数体的语句，把所有申明的变量“提升”到函数顶部

```
function foo() {
    var x = 'Hello, ' + y;
    alert(x);
    var y = 'Bob';
}

//提升后相当于
function foo() {
    var y; // 提升变量y的申明
    var x = 'Hello, ' + y;
    alert(x);
    y = 'Bob';
}
```
>**语句var x = 'Hello, ' + y;并不报错，原因是变量y在稍后申明了。但是alert显示Hello, undefined，说明变量y的值为undefined。这正是因为JavaScript引擎自动提升了变量y的声明，但不会提升变量y的赋值**

### 全局作用域

不在任何函数内定义的变量就具有全局作用域，JavaScript默认有一个全局对象window，全局作用域的变量实际上被绑定到window的一个属性

```
var course = 'Learn JavaScript';
alert(course); // 'Learn JavaScript'
alert(window.course); // 'Learn JavaScript'
```
>JavaScript实际上只有一个全局作用域。任何变量（函数也视为变量），如果没有在当前函数作用域中找到，就会继续往上查找，最后如果在全局作用域中也没有找到，则报ReferenceError错误。

### 命名空间

全局变量会绑定到window上，不同的JavaScript文件如果使用了相同的全局变量，或者定义了相同名字的顶层函数，都会造成命名冲突；减少冲突的一个方法是把自己的所有变量和函数全部绑定到一个全局变量中。

```
// 唯一的全局变量MYAPP:
var MYAPP = {};

// 其他变量:
MYAPP.name = 'myapp';
MYAPP.version = 1.0;

// 其他函数:
MYAPP.foo = function () {
    return 'foo';
};
```

### 常量

var和let申明的是变量，如果要申明一个常量，在ES6之前是不行的，ES6标准引入了新的关键字const来定义常量

```
const PI = 3.14;
PI = 3; // 某些浏览器不报错，但是无效果！
PI; // 3.14
```

## 方法

绑定到对象上的函数称为方法，它在内部使用了一个this关键字，this是一个特殊变量，它始终指向当前对象。

```
function getAge() {
    var y = new Date().getFullYear();
    return y - this.birth;
}

var xiaoming = {
    name: '小明',
    birth: 1990,
    age: getAge
};

xiaoming.age(); // 25, 正常结果
getAge(); // NaN
```	

## 高阶函数

JavaScript的函数其实都指向某个变量。既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数

```
function add(x, y, f) {
    return f(x) + f(y);
}
add(-5, 6, Math.abs);//11
```

### map函数

调用Array的map()方法，传入我们自己的函数，就得到了一个新的Array作为结果

```
function pow(x) {
    return x * x;
}

var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
arr.map(pow); // [1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### reduce函数

reduce()把一个函数作用在Array的[x1, x2, x3...]上，把结果继续和序列的下一个元素做累积计算`[x1, x2, x3, x4].reduce(f) = f(f(f(x1, x2), x3), x4)`

```
var arr = [1, 3, 5, 7, 9];
arr.reduce(function (x, y) {
    return x + y;
}); // 25

要把[1, 3, 5, 7, 9]变换成整数13579
var arr = [1, 3, 5, 7, 9];
arr.reduce(function (x, y) {
    return x * 10 + y;
}); // 13579
```

### filter函数

用于是把Array的某些元素过滤掉，然后返回剩下的元素。

Array的filter()接收一个函数,把传入的函数依次作用于每个元素，然后根据返回值是true还是false决定保留还是丢弃该元素。

```
//在一个Array中，删掉偶数，只保留奇数
var arr = [1, 2, 4, 5, 6, 9, 10, 15];
var r = arr.filter(function (x) {
    return x % 2 !== 0;
});
r; // [1, 5, 9, 15]

//去除Array的重复元素
var r,arr = ['apple', 'strawberry', 'banana', 'pear', 'apple', 'orange', 'orange', 'strawberry'];
r = arr.filter(function (element, index, self) {
    return self.indexOf(element) === index;
});
```

### sort函数

sort()方法默认把所有元素先转换为String再排序。sort()方法会直接对Array进行修改，它返回的结果仍是当前Array。

```
['Google', 'Apple', 'Microsoft'].sort(); // ['Apple', 'Google', 'Microsoft'];

['Google', 'apple', 'Microsoft'].sort(); // ['Google', 'Microsoft", 'apple']

[10, 20, 1, 2].sort(); // [1, 10, 2, 20]
```
sort()方法也是一个高阶函数，它还可以接收一个比较函数来实现自定义的排序

```
var arr = [10, 20, 1, 2];
arr.sort(function (x, y) {
    if (x < y) {
        return -1;
    }
    if (x > y) {
        return 1;
    }
    return 0;
}); // [1, 2, 10, 20]
```

## Arrow Function

ES6标准新增了一种新的函数：Arrow Function（箭头函数）它的定义用的就是一个箭头

```
x => x * x
相当于
function (x) {
    return x * x;
}

// 两个参数:
(x, y) => x * x + y * y

// 无参数:
() => 3.14

// 可变参数:
(x, y, ...rest) => {
    var i, sum = x + y;
    for (i=0; i<rest.length; i++) {
        sum += rest[i];
    }
    return sum;
}
```