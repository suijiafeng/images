title: js的简单总结
author: suijiafeng
tags: []
categories: []
date: 2017-02-13 01:31:00
---


### JS的数据类型

1. 简单基本数据类型 :number  boolean  string  
2. 复杂数据类型: Array  function  Object   Date  RegExp    Math   String    Number   Boolean
3. 空类型   :  null  undefined
4. 基本包装类型 ：Number  String  Boolean

## 显式数据转换
-Boolean|(需要转换的内容）
    a:可以转换成false的有： 0  -0  false  undefined  null  NaN   ""空字符串

## Number()函数   可以用于任何数据类型
- 如果是Boolean 值，true和false将分别被转换为 1 和 0
- 如果是数值，只是简单的传入和返回。
- 如果是null ，返回的是 0
- 如果是undefiend   那么返回的是 NaN。
- 如果是字符串，那么遵从如下规则：
>     1.如果字符串本身的值是一个数字，就可以转换成数字。
>     2.如果就是一个字符串，那么转换成 NaN
>     3.如果字符串是一个空格字符串" ",或者是一个空字符串""，转换成0。
>     4.如果字符串本身的值是一个数字，头尾有空格会忽略，会被转换成一个数字；但是如果 中间有空格，那么会转成 NaN.  比如说：  var str = " 3 2 ";
>     5.如果字符串本身的值是一个小数，那么会转换成小数。

## parseInt()函数 用于把字符串转换成数值
> 从左到右，找到是数字的部分，把他转换。
> 如果字符串的值本身是一个小数，转换后得到的是他的整数部分。


## parseFloat()函数  用于把字符串转换成数值
如果字符串的值本身是一个小数，注意：转换后得到的就是这个小数本身。

## 如何保留小数的位数
    可以先放放大若干倍数，在做相对应的操作。
    
## 隐式转换
- 其他类型的转number ---在需要转换的内容前面写一个正号 +，适用规则和Number()函数的转换规则一样。
- 其他类型转换string ：----使用连接符+
- 其他类型转布尔类型 ：----使用取反运算符 --语法  !!需要转换的内容

### valueof ()

是拿到对象原始的值

### toString()

对象的 toString()   ---[object type]

数组的 toString()

转换为字符串类型

### 其它：

如果一个复杂的数据类型和一个基本的数据类型进行运算，会调用这个对象的valueOf方法，取去他的原始值再和这个基本数据类型进行运算.


<html>
    <script>
        console.log([] == ![]); //true
        console.log({} == !{}); //false
    </script>
</html>

  如果valueOf取不到一个值，就调用这个对象的toString方法，得到的值再和这个基本数据类型进行运算。



### 判断数据类型

a  typeof

能够判断基本数据类型(除了null，null会得到一个object)。 以及函数。

b  instanceof

 可以判断数据类型，不严谨


### continue  

跳出本次循环

### break 

直接跳出循环体

### 对象的动态特性

1. 动态的给对象添加属性和方法
2. 可以使用点语法
3. 可以使用数组特性的方式



## DOM元素操作

 在地址栏上也是可以输入js代码的 ，同样也是可以执行的

谷歌浏览器输出结果看颜色判断是什么类型。

number:蓝色  string :黑色

## navigator 

 navigator .userAgent 查看浏览器信息

### 循环

for()

for(var key in obj)

### in 关键字的使用

a 可以用来循环数组与对象

b 判断某个对象是否可以访问某个属性、方法

语法： "属性名" in  对象

c  判断数组中有没有这个下标

 "下标" in 数组

## 值类型作为函数的参数

执行过程分析：

举个例子：

 function test1(num){

   num = 100;

 }

 var num1 = 10;

 test1(num1);

 console.log(num1); //10

 1 先声明一个变量 var num1 =10;

2 函数如果有形参，会先声明形参。

3 把实参的值复制一份给形参。

4 执行函数体

## 引用类型作为函数的参数

### 逻辑中断

逻辑与 &

找假：

如果参入逻辑运算的的第一个式子能够转换成布尔类型的false那么整个逻辑与表达式的结果就是第一个式子的值，如果第一个式子的值不能转换成布尔类型的false，那么整个逻辑与表达式的结果就是第二个式子的值。

逻辑或 ||

找真

如果参入逻辑运算的的第一个式子能够转换成布尔类型的true那么整个逻辑与表达式的结果就是第一个式子的值，如果第一个式子的值不能转换成布尔类型的true，那么整个逻辑与表达式的结果就是第二个式子的值。

### delete关键字的使用

-  删除那些没有用 var 关键字声明的变量

语法：  delete 变量

-  删掉某个元素，后面的那些元素不会自动的往前移动


var arr = [10,20,30,40];

delete arr[0];

console.log(arr);//下标为0  的元素已经被删除，但是位置仍然保留。

-  移除对象的属性：

  语法：  delete 对象名.属性名
  
## removeAttribute
普通的对象没有removeAttribute()方法，只有dom对象才有这个方法。
```
//removeAttribute dom对象移除属性
//obj.removeAttribute("age"); //报错，普通的对象没有removeAttribute()方法，只有dom对象才有这个方法。
//console.log(obj);

```

  

### 数组操作

//  arr.pop(); //删掉最后一个

//  arr.push(); //往数组的最后一个添加元素

//  arr.shift(); //删掉第一个

//  arr.unshift(); //往数组的第一个添加元素

### 异常处理

如果程序在某一个地方出了异常，那么这个地方后面的代码都不会执行。

 //2.捕获异常，做处理

  //语法： try {

  //         有可能会出现异常的代码

  //      }catch(e){

  //         捕获到异常了之后要执行的处理-代码

  //         e就是异常信息

  //      }finally {

  //         不管有没有发生异常，都要执行的代码

  //         释放资源的处理

  //      }

  //如果try里面的代码没有发生异常，就执行try里面的代码，不会执行catch里面的代码。

  //如果try里面的代码发生了异常，就不执行try里面的代码，会执行catch里面的代码，e是异常信息。

  //finally里面的代码不管有没有发生异常都要执行。



## 逻辑与表达式

关键字：找假
在一个逻辑与表达式中，如果第一个式子能够转换成false的话，那么第一个式子的值就是整个表达式的值。如果不是那么最后一个式子的值是整个表达式的值。

```
var num1=10,num2=20;
var res = num1>0&&num2>0;
console.log(res);//true

var num3=10,num4=20;
var res = num3&&num4;
console.log(res);//20

var num5=10,num6=20;
var res = num5<0&&num6;
console.log(res);//false

```

## 逻辑或表达式

关键字：找真
在一个逻辑或表达式中，如果第一个式子能够转换成true的话，那么第一个式子的值就是整个表达式的值。
```
 var num1 = 10;
 var num2 = 20;
 var res = undefined || num2++;
 console.log(res); //20
 console.log(num2); //21

```
 
## 逻辑与 与 逻辑或的应用
```
var value1 = document.getElementById("one")  && document.getElementById("one").value ;


分析：如果不存在这个 one这个选择器 那么value1 =null ,如果存在，那么返回这个选择器相对应的值..
好处，不至于报错。

```






















