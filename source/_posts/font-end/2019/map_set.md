---
title: ES6中的数据结构
tags: 前端 数据结构
date: 2019-09-21 10:00:05
categories: front-end
---

ES6之前JS中能用到的数据结构就是`Array`和`Object`。通过数组`Array`来模拟多种结构比如，
> 通过push+pop 或者 shift + unshift来模拟栈的操作; 通过push+shift 或者 unshift + pop来模拟队列的操作。

Array有很丰富的API，但是数组去重，一直是一个很常见的问题。

Object是一个键值对的结构。JavaScript 的对象（Object），本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键。这给它的使用带来了很大的限制。

<!-- more -->

ES6给我们提供了Map和Set两种数据结构，让JS的数据结构能力有了更大的提升。

## Set
ES6 提供了新的数据结构 `Set`。它类似于数组，但是成员的值都是唯一的，没有重复的值。

`Set`本身是一个构造函数，用来生成 `Set` 数据结构。

`Set`对成员值是否重复用的方式是`===`。
   - 两个NaN是相等的
   - 两个对象总是不相等的


### Set的属性和方法

Set的属性:
 - Set.prototype.constructor: 构造函数，默认就是Set函数
 - Set.prototype.size: 返回`Set`实例的成员总数
 
 Set的方法分为两大类，操作方法和遍历方法。
 
 - 操作方法
     - Set.prototype.add(value):添加某个值，返回Set结构本身
     - Set.prototype.delete(value):删除某个值，返回一个布尔值，表示删除是否成功
     - Set.prototype.has(value): 返回一个布尔值，表示该值是否为Set成员
     - Set.prototype.clear(): 清楚素有成员。没有返回值
     
- 遍历方法
    - Set.prototype.keys():返回键名的遍历器
    - Set.prototype.values(): 返回键值的遍历器
    - Set.prototype.entries(): 返回键值对的遍历器
    - Set.prototype.forEach():使用回调函数遍历每个成员 
> 由于Set结构没有键名，只有键值（或者说键值和键名是同一个值），所以`keys()`方法和`values()`方法的行为完全一致。

### WeakSet
   WeakSet 结构与 Set 类似，也是不重复的值的集合。但是，它与 Set 有两个区别。

 - 首先，WeakSet 的成员只能是对象，而不能是其他类型的值。

 - 其次，WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。

WeakSet内的对象，随时都可能被垃圾回收，所以WeakSet不可遍历，只有三种方法
- Set.prototype.add(value): 添加成员
- Set.prototype.has(value): 返回布尔值，表示某个值是否在WeakSet中
- Set.prototype.delete(value): 清楚WeakSet实例的指定成员，

## Map
`Map`类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。

### Map的属性和方法
 - Map.prototype.size
 - 操作方法
     - Map.prototype.set(key, value)
     - Map.prototype.get(key)
        get方法 读取key对应的键值，如果找不到key，返回undefined。
     - Map.prototype.has(key)
     - Map.prototype.delete(key)
   - Map.prototype.clear()
 - 遍历方法
     - Map.prototype.keys(): 返回键名的遍历器。
     - Map.prototype.values(): 返回键值的遍历器
     - Map.prototype.entries(): 返回所有成员的遍历器
     - Map.prototype.forEach(): 遍历Map的所有成员


### WeakMap
WeakMap与Map的区别有两点。
- 首先，WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名。
- 其次，WeakMap的键名所指向的对象，不计入垃圾回收机制。

WeakMap是无法遍历的，所以只有四个方法可以使用
- Set.prototype.set(key, value);
- Set.prototype.get(key);
- Set.prototype.has(key);
- Set.prototype.delete(key);


## 实战应用

### 利用Set完成数组(字符串)去重

```js
    let arr = [1,2,3,3,4,4,5,6,6];
    let str = 'abccdd33bbaa'

    arr = [...new Set(arr)];
    str = [...new Set(str)].join('');
```

### 利用WeakMap不被引用计数
```js
let myWeakmap = new WeakMap();

myWeakmap.set(
  document.getElementById('logo'),
  {timesClicked: 0})
;

document.getElementById('logo').addEventListener('click', function() {
  let logoData = myWeakmap.get(document.getElementById('logo'));
  logoData.timesClicked++;
}, false);
```

### Map类型互换
```js
    const myMap = new Map()
          .set(true, 7)
          .set({foo: 3}, ['abc']);
    //Map转数组
    let arr = [...myMap]; //[ [ true, 7 ], [ { foo: 3 }, [ 'abc' ] ] ]
    
    //对象转Map
    let obj = {"a":1, "b":2};
    let map = new Map(Object.entries(obj));
    
```