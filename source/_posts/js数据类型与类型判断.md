---
layout: '[layout]'
title: js数据类型与类型判断
date: 2019-05-29 14:29:48
categories: JavaScript
tags: 基本数据类型,JavaScript,js类型判断
---
### 数据类型

* ECMAScript有5种基本数据类型：Undefined、Null、Boolean、Number、String。
object属于复杂数据类型，因此js有六种数据类型。(es6中添加Symbol类型)

+ 检测数据类型：使用 typeof 检查一个变量的数据类型。
    - 检查有一个变量没有赋值时，数据类型为 undefined。
    ```js
    // 当变量不赋值时，自动赋值为undefined
    var aa ;
    console.log(typeof aa);//undefined
    ```
    - 使用 typeof 检查 null 时无效，因为 null 属于 object 类型。因此一般在判断中不适用 typeof null
    ```js
    var bb = null;
    console.log(typeof bb);//object
    ```
#### undefined 类型 

* undefined类型只是一个值，使用var声明一个变量时没有初始化时的值。
#### null 类型
* null类型是只有一个值的类型。值为null,从逻辑上来看null值表示一个空对像指针，也是 typeof 检查 null 值
会返回object的原因。如果一个变量要用来保存一个对象初始化就可以是null,而不是其他类型。
#### boolean 类型
 * 该类型只有两个值，true和false。【注：true不一定等于1，false不一定等于0】,将其他类型的变量转为boolean类型
```js
    //将一个变量转为boolean类型
    var b1 = 'hello',b2,b3 = 1,b4 = 0;
    var bb1 = Boolean(b1);
    var bb2 = Boolean(b2);
    var bb3 = Boolean(b3);
    var bb4 = Boolean(b4);
    console.log(bb1)// true
    console.log(bb2)// false
    console.log(bb3)// true
    console.log(bb4)// false
```
数据类型|转换为true的值|转换位false的值
:----:|:-----:|:-----:
Boolean|true|false
String|任何非空字符|""（空字符串）
number|任何非零数字|0和NaN
object|任何对象|null
undefined|不适用|undefined

#### number类型
* number 使用IEEE754表示整数和浮点数。
* 数值转换：可以使用Number(),parseInt(),ParseFloat()进行转换。第一个可以转换任何类型的数据，有两种是转换字符串类型。

#### String 类型
* string 类型用于表示0或多个unicode字符组成的字符序列。
* 将其他类型的转换位string类型，可以使用toString()方法，但是null和undefined没有toString()方法，只能使用String(null)返回得到字符串'null'。数字类型转为string可以加一个空字符串''。

#### object 类型
* 其实是一组数据和功能的集合。可以使用 new 来创建一个对象。var o = new Object();
+ 主要函数
    - constructor 保存着用于创建当前对象的函数，即构造函数。
    - hasOwnProperty(propertyName) 检查给定的属性名是否在当前对象中。参数必须是字符串。
    - isPrototypeOf(object) 检查传入的对象是否是当前对象的的原型。
    - propertyIsEnumerable(propertyName) 检查给定属性是否可以使用for-in语句来枚举。
    - toLocaleString() 返回对象的字符串表示。
    - toString() 返回对象的字符串表示。
    - valueOf() 返回对象的字符串、数组或布尔值表示。

### 类型检查

#### 判断js数据类型的方法
* 判断js的数据类型有四种，分别是typeof、instanceof、constructor、toString。
##### typeof 方法
* typeof 可以检查以下7种类型number、boolean、string、object、undefined、function、symbol。此方法返回的事被检测的类型名称。

```js
    // 检查字符串
    var str = 'str';
    console.log(typeof str) // string

    // 检查数字
    var num = 3;
    console.log(typeof num); // number

    // 检查 boolean 类型
    var bool = false;
    console.log(typeof bool); // boolean

    // 检查 undefined 类型
    var un;
    console.log(typeof un); // undefined

    // 检查 null 类型
    console.log(typeof null); // object

    // 检查 object 类型
    var obj = new Object();
    console.log(typeof obj); // object
    
    // 检查 function 类型
    var fun = function () {};
    console.log(typeof fun); // function
    
    // 检查 Symbol 类型
    let s = Symbol();
    console.log(typeof s); // Symbol
```
【注】
* 对于基本类型number、boolean、string、null、undefined 只有null返回object，其他返回类型正常。
* 对于引用类型，除 function 以外，一律返回 object 类型。

对于null返回object是因为null的直属类型是object，返回了处于其原型链最顶端的 Object 类型

#### instanceof 方法

* instanceof 是判断a是否为b的实例，使用表达式 a instanceof b ,返回true和false，如果a属于b返回true，不属于就返回false。检查的是原型。

```js
    // instanceof 检查
    var dd = new Date();
    console.log(dd instanceof Date)// true

    console.log(null instanceof Object) // true

    var str = '';
    console.log(str instanceof Number) // false
```

#### constructor

* 当一个函数被定义时，JS引擎会为此函数添加 prototype 原型，然后再在 prototype上添加一个 constructor 属性，并让其指向这个函数的引用。

```js
    function Fun() {
       console.log('hello world')
    }
    var f = new Fun();
    console.log(f.constructor == Fun) // true
```

【注】null 和 undefined 是无效的对象，因此是不会有 constructor 存在的。一般用来检查自定义的函数。当使用 prototype 重写后，原有的 constructor 引用会丢失，constructor 会默认为 Object

#### toString
使用toString判断 Object 对象，直接调用 toString()  就能返回 [object Object] 。而对于其他对象，则需要通过 call / apply 来调用才能返回正确的类型信息。
```js
    var obj = {};
    console.log(obj.toString())// [object Object]
    console.log(Object.prototype.toString.call('')) // [object String]
    console.log(Object.prototype.toString.call(2)) // [object Number]
    var array = [];
    console.log(Object.prototype.toString.call(array)) // [object Array]
```
