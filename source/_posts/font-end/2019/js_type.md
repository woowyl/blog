---
title: 0 == false ？
date: 2019-10-23 21:00:05
categories: front-end
tags: 
- 前端
---

在javaScript中，经常会看到 `0 == false` => ture的情况，一个Number类型，怎么能等于一个Boolen类型呢？先从javaScript的基本类型说起
<!-- more -->
## javasript类型
### 类型分类
传统意义上我们会说是7中基本类型，Number String Boolean undefined null Symbol Object。

目前还在推进阶段的Bigint类型。除了这种分类之外，我们还可以有一个更详尽的分类方式：
- 6中原始类型
     - Number
     - String
     - Boolean
     - undefined
     - Symbol
     - Bigint
- Object 引用类型
    - Array
    - Object
    - Map
    - Set
    - Date
    - ...
- null
- Function

###  类型判断
如何判断当前变量的类型呢，将JS常用的几种方式，做一个归纳：

- 原始类型 用 `typeof`
    - undefined：`typeof instance === "undefined"`
    - Boolean：`typeof instance === "boolean"`
    - Number：`typeof instance === "number"`
    - String：`typeof instance === "string`
    - BigInt：`typeof instance === "bigint"`
    - Symbol ：`typeof instance === "symbol"`
 
- 引用类型 
    - 可以统一用 `Object.prototype.toString.call(ins)` 分别得到以下内容
        - Null: `'[object Null]'`
        - Object：`'[object Object]'`
        - Array：`'[object Object]'`
        - Set：`'[object Set]'`
        - Map：`'[object Map]'`
        - Function: `'[object Function]'`
        - Date: `'[object Date]'`
        - RegExp: `'[object RegExp]'`
        - ...
    - 也可以用用一些单个API
        - Object
        - Array:
            - `Array.isArray(arr)`
            - `arr instanceof Array`'
         - null
      - Function
           - `typeof Function === 'function'`


###  类型转换

|-     |Number|String|Boolen|Undefined|Null|Object|Symbol|
|-      |-    |    -|-    |-    |-    |-     |-    |
|Number  |-   |     |0=>false| x   |  x  |Boxing|  x   |
|String  |    |-   |""=>false| x   |  x  |Boxing | x   |
|Boolean | true=>1 false=>0   | true=>'true' false=> 'false'    |-        |x    | x  | Boxing | x  |
|Undefined| NaN| 'undefined'|  false  |-    | x  |      | x   |
|Null    | 0 | 'null' | false   |x    |-   |      | x  |
|Object  | valueOf   | valueOf toString    |  true        |x    | x    |-    | x   
|Symbol  | x  |  x  | x     |x    | x    |  Boxing |-    |


 
#### unboxing & boxing

装箱和拆箱，是在java中提到的概念，在理解这个之前，要首先明白，在JS里类和类型是两个不同的概念。 这是一些动态语言的特性，比如javaScript、python。Javascript有7种基本类型，其中，`Number`、`String`、`Boolen`、`Symbol`又拥有各自的类。这里要特别注意区分类和类型的区别,虽然，`new String('hello').lenth == 'hello'.length` ，但是他们的`typeof`并不相同：
```js
    typeof new String('hello')    //object
    typefo 'hello';              //string
    
    !new String('')  //false
    !''             //true

```
除了，new操作之外，`Number`、`String`、`Boolean`不带new操作还可以直接进行类型转换,得到的并不是object,而是转换后的类型本身
```js
    Number('1')   => 1
    String(2222)  => '22222' //这里返回的是string类型，而不是String对象
    Boolen(1)     => true
    Boolen('0')   => true
    Boolen(0)     => false
    Boolen('')    => false
```

> 这里推荐大家不要用自动的类型转换，涉及到类型转换的地方，都显式地采用手动的类型转换，对可读性比较有帮助。

这里有一个比较特殊的类型`Symbol`，是new不了的。

##### boxing
装箱就是一个操作的统称，指的是将一个基础类型转换为其对应的Object类型，除了上面提的`new`操作之外，也可以通过`Object(类型变量)`来实现装箱。
 ```js
    //装箱操作1
    Object('hello')
    //装箱操作2 new
    new String('hello')  //String obj
```

可以装箱操作的类型有: `Number`、`String`、`Boolean`、`Symbol`;其中`Symbol`无法采用new的方式，其他的三类两种方式均可。

装箱操作一般是需要手动完成得，而在自动类型转换中，会经常遇到拆箱操作

##### unboxing
拆箱操作是在将`Object`对象转换为其他基础类型时发生的操作。当进行拆箱操作时，将自动调用`[Symbol.toPrimitive]`，`ValueOf`，`toString`三者中的一个，调用的原则是：
1. 存在 `[Symbol.toPrimitive]`时，按照`[Symbol.toPrimitive]`函数进行转换
2. 没有`[Symbol.toPrimitive]`的顺序是
    1.`ValueOf()`
    2.`toString()`
3. 当且仅当`ValueOf()`仍然返回Object时，将调用toString函数
4. 你很少需要自己调用`valueOf`方法；当遇到要预期的原始值的对象时，JavaScript会自动调用它。
举例说明：
```js
    
    var obj1 = {
        [Symbol.toPrimitive](){
            return 1;
        },
        valueOf() {
            return 2;
        },
        toString() {
            return 3;
        }
    }
    
    console.log(1 + obj1);      // 2
    
    
    var obj2 = {
        valueOf() {
            return 2;
        },
        toString() {
            return 3;
        }
    }
    
    console.log(1 + obj2);      // 3
    
     var obj3 = {
        toString() {
            return 3;
        }
    }
    
    console.log(1 + obj3);      // 4
    
     var obj4 = {
        valueOf() {
            return {};
        },
        toString() {
            return 3;
        }
    }
    
    console.log(1+obj4);         //4
    
    
      var obj5 = {
        valueOf() {
            return '222';
        },
        toString() {
            return 3;
        }
     }
    
    console.log(1+obj5);         //1222

```



##### toString toLocaleSting的常见用法

在object对象中已经内置了toSting 和 toLocalString方法，但是你可以重写他们。

- toString()

    每个对象都有一个 toString() 方法，当该对象被表示为一个文本值时，或者一个对象以预期的字符串方式引用时自动调用。默认情况下，toString() 方法被每个 Object 对象继承。如果此方法在自定义对象中未被覆盖，toString() 返回 "[object type]"，其中 type 是对象的类型。以下代码说明了这一点：
    
```js
    var o = new Object();
    o.toString(); // returns [object Object]
```

在进制转换中也可以使用toString()的方式

```js
    Number(12).toString(2)  // 1100
    Number(12).toString(进制)
    //逆向操作
    parseInt(1100,2)    //12
```
  
- valueOf()

|对象	|返回值|
|-|-|
|Array	|返回数组对象本身。|
|Boolean|	布尔值。|
|Date|	存储的时间是从 1970 年 1 月 1 日午夜开始计的毫秒数 UTC。|
|Function|	函数本身。|
|Number|	数字值。|
|Object|	对象本身。这是默认情况。|
|String	|字符串值。|
|	|Math 和 Error 对象没有 valueOf 方法。|

- toLocaleString()
toLocaleString 不同于前两个API，它并没有类型转换的效果，但是有一些小技巧，在我们日常开发中十分有用。

```js
    1234567 .toLocaleString();  // "1,234,567"
    
    
    const event = new Date(Date.UTC(2012, 11, 20, 3, 0, 0));
    onsole.log(event.toLocaleString('en-GB', { timeZone: 'UTC' }));// 20/12/2012, 03:00:00
```
Array.prototype.toLocaleString()返回一个字符串表示数组中的元素。数组中的元素将使用各自的 toLocaleString 方法转成字符串，这些字符串将使用一个特定语言环境的字符串（例如一个逗号 ","）隔开。

## 3.2 String to Number
javaScript 已经有了Strign to Number的api： 
 - parseInt/parseFloat
 - Number
 - 字面量1231
这些api的使用方式和最终结果，有或多或少的不同。


## Number to String


##  ===

## 参考文献

[Symbol.toPrimitive](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toPrimitive)