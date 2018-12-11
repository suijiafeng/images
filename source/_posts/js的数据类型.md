title: js的数据类型
author: suijiafeng
tags: []
categories: []
date: 2017-05-10 01:11:00
---


### 特点：弱类型特性。

共有5种原始类型：number String  boolean null undefined  

1中Object 类型

### 隐士转换：

#### + - 巧用 + - 的转换逻辑 

```text
"123"==123

0 ==false

null ==undefined

[1,2]==[1,2]  因为他们两个是不同的对象

NaN 不等于NaN

```

​	类型相同，同 ===

​	类型不同，尝试类型转换

### 包装对象

object 对象 ：Function   Data  Array

当我们尝试把基本类型当成是对象来使用的时候 

​	js内部会帮我们包装成对象，当这个动作完成后，这个对象也就被销毁了

```
var a = "string";
undefined
a.length
6
a.t=3;
3
a.t;//设置完 a.t 属性之后，临时被包装的对象也就被销毁了。
undefined

```

### 类型检测

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/FB4BBE59F1EA4502A382B894597A67E7/3984)

### obj instanceof Object 

运行原理：判断左边obj 对象的原型链上是否有右边这个对象 Object 的protype 属性

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/41AC3A6387BF4C58B4C0A66425E10FA7/4009)

类型检测：

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/C752C7F7F0CF4193A0F573FBB45C118C/3983)

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/436627D93CD84BA5B105A95C5EC464D4/3976)

## 表达式：

 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/6E53834BD4B3462CA38EBF41176871A2/4001)

 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/31D3784199B141E0926812709C719CB7/4008)

 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/76EB0C738F2244E297CB8BFE9EC7DD41/4007)

## 函数表达式

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/7D18A95A288643A99D24A92679056300/4004)

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/54A02DEA8BBD4D9C96E7BE5CDB23B1FF/4000)
 
 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/F9D6DD9AC2BE4761A65788A1058402B8/4011)

 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/4818F9BEA00D434C95AD9135464A021C/4012)
 
 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/31D3784199B141E0926812709C719CB7/4008)

## 运算符：

 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/321866938F70466E8D2F8E7D63DBA93E/3991)

1.三元运算符

2.逗号运算符   var val=(1,2,3);//3

3.delete 
![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/333B88DF0E8748AFB86585161D36C27C/4005)

4 in 

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/7B8CC053B0C74C219262FC4561286350/4014)

5 new 

 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/079255AA1ABE43ED9C6D54664CE2ECB7/3989)



6 this 

7 void

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/305B1F06510E417D97C139005F603CBE/4006)

### 运算优先级

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/68CCC9C97DC147B7AFF8B1301755A057/3985)

## 语句 
![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/CC3CE85350AC49BAA884FC513E06C8BD/4010)

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/D130CDE1FBA04263BC98D543EA9474E2/3999)

 ### 语句种类![语句种类](img\语句种类.png)


![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/594D6B06E1ED499B8A8B35E2E2E59B3E/3978)

```
浏览器把 {a:1,b:2}//当成了块，而不是对象字面量。
```

	## var 声明语句

var a;

var a,b,c;

## try catch

 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/9A2D2E9131384D599C8D0A77E4575B77/3997)

1 首先执行try 中的代码，如果出现异常就由catch 捕获，但是不过有没有异常，最后都会执行finally 中的代码

2 注意点：try  后面一定要带一个catch 或finally ,或者两者皆带。



## function

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/CA85762E97AD42F1944B8440E8B6708A/3998)

## for in 

 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/7F60F0525096436FA4C14C6A97F7BEF6/3992)

## switch

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/93DEF6B7D89947AD84EBD1FB4EBD497C/3977)

 ##循环

 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/0A771B6BB11B4433B978B6EFB1CB2F39/3996)

## with

可以修改当前的作用域

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/DE66C7F7A6F84651AA1FE316AFBB8B3A/3986)

## 严格模式

 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/402FB559EF664368B75A203250D89EC0/3980)

### 严格模式下的特点：

```text
SyntaxError :语法错误
ReferenceError:引用错误
```

 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/2C7DAA3A206D45CC8CA318D94A9F8D6F/3981)
 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/9DAE9D1097764EA59F637296832083E5/3982)
 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/91F5F9BC36444D37BC30F3FDA1EF7C0D/3993)
 
 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/4DAAF4083AE548599AEED43A75996AB8/3987)
 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/43A17FEC60E94241B5B04230098936F3/3972)
 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/01EB9BB7B8604F00B12263C7092252C1/3990)
 
 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/CD2D2F645F444DA98F9B8DDF35629B79/3979)
 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/ADA09EEEDC534D8BBD15294F47CC2451/3994)
 ![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/F16D3979C84F486898129F1F1C732215/3988)


## 对象

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/1EDEBD03D3444A939F562266508E921F/3995)

## 对象结构

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/45D357D6CE7B42F9A03147E9F6490BFB/3973)

 ## 创建对象

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/12011010BC4D48A5B5E79B0FFB5C3D12/4003)

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/5B2424434354487EA567EE30A6755468/3974)
 

创建对象的方式2-new 原型链--深入理解

![image](https://note.youdao.com/yws/public/resource/6032a8a4d7150d5aafd6a0153265cf44/xmlnote/5B2424434354487EA567EE30A6755468/3974)











