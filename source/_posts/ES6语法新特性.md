---
title: ES6语法新特性
tags: 
  - js
categories: 
  - 技术
date: 2026-03-19
---



### let 和 const 命令

+ `let `声明的变量在代码块内有效

+ `let `不允许重复声明

+ `let `不存在变量提升

  ```js
  console.log(a);        
  var a = 1; // 输出undefined
  console.log(b);        
  let b = 1; // 报错Uncaught ReferenceError
  ```

+ `const`  声明只读的常量

+ `const` 一旦声明变量，就必须立即初始化,不能留到以后赋值

  ```js
  const person = {name:'mjj'};// 可以修改变量成员
  person.name = 'alex';
  console.log(person); // {name:'alex'}
  ```

  **在默认情况下用`const`,而只有你在知道变量值需要被修改的情况下使用`let`**

### 字符串的操作

使用`${变量名}`来替换字符串

```
var name = 'mjj';
var htmlTel = `<p>name:${name}</p>`
```

### 箭头函数

- 使用 () => {} 代替 function (){}

-  箭头函数没有this的指向，箭头函数内部的this值只能通过查找作用域链来确定
-  如果箭头函数被一个非箭头函数所包括，那么this的值与该函数的所属对象相等，否则 则是全局的window对象
- 箭头函数中没有arguments对象 
- 箭头函数不能使用new关键字来实例化对象

```js
let add = function (a,b){return a+b}; 
let add2 = (a,b) => {a+b}; // 箭头函数

let add3 = (a,b=20) => {a+b} //带参数默认值的函数
let add4 = (a,b=add(1,2)) => {a+b} //参数默认值可以是函数

let checkArgs = (...args) => {console.log(args);} //...args 剩余参数
checkArgs('a', 'b', 'c');

var arr = [10, 30, 20];
console.log(...arr); //扩展运算符
```

### 对象的扩展

属性，方法的简洁表示法

```js
const name = '张三';
const age = 19;
//es5
var person = {
    name:name,age:age,sayHi:function(){console.log('hi')}
}
//es6
let person = {
    name,age,sayHi(){console.log('hi')}
}
```

   属性名表达式

```js
obj={};
obj['a' + 'bc'] = 123;
obj['a'+'v'] = (aa)=> aa; //输出 {abc: 123, av: ƒ}

// assign() 合并对象
let obj1 = {a: 1};
let obj2 = {b: 2};
let obj3 = Object.assign(obj1, obj2); //输出 {a: 1,b: 2}
```



### 解构赋值

1. 对象结构

```js
let node = {type:'identifier',name:'foo'}
let {type,name} = node;
console.log(type,name); // 输出 identifier foo

let {a,b = 10} = {a:20}; // 默认值
console.log(a,b); // 输出 20 10
```

2. 数组

```js
let arr = [1,2,3];
let [a,b,c] = [1,2,3];
console.log(a,b,v); // 输出 1 2 3
```

**Symbol**

> Symbol类型，它表示独一无二的值
>
> 最大的用途 是用来定义对象的私有成员

### Map 和 Set

##### Set

Set类型，一种无重复值的有序列表

```js
let set = new Set(); //创建set对象
set.add(5);          // 添加元素
set.delete(5);       //移除元素
set.clear();         //清空
console.log(set.size);//size属性来访问该集合的长度
console.log(set.has(5));//has()方法来校验某个值是否存在于Set中
//forEach()方法
set.forEach(function(val,key,ownerSet) {
    console.log(key,val); 
    console.log(ownerSet);  
    }) 
//转换为数组
let set = new Set([1,2,3,3,4,5]);
let arr = [...set];

//set中的对象引用无法被释放
```

##### Weak Set

> 解决set中的对象引用无法被释放
>
> `WeakSet` 的成员只能是对象，而不能是其他类型的值。
>
>  size、`forEach`、clear 方法都不存在

```js
const ws = new WeakSet();
const a = [[1, 2], [3, 4]];
const ws = new WeakSet(a); // WeakSet {[1, 2], [3, 4]}
```

#####  Map

  Map类型是键值对的有序列表，而键和值都可以是任意类型

```js
let map = new Map();
map.set('name','张三');// set()方法 相当于设置值
map.delete('name');
map.has('name');
map.size;
map.clear();
map.forEach(function (val,key,ownerMap) {
        console.log(key,val);
        console.log(ownerMap); 
    })
```

##### Weak map

> `WeakMap`只接受对象作为键名（`null`除外），不接受其他类型的值作为键名

```js
const wm1 = new WeakMap();
const key = {foo: 1};
wm1.set(key, 2);
wm1.get(key);
// size、forEach、clear 方法都不存在
```

