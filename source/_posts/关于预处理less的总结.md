title: 关于预处理less的总结
author: suijiafeng
tags: []
categories: []
date: 2016-01-22 01:02:00
---
## css 使用方式 ## 
### 行内样式 ###
    直接写在html 标签里面的 
### 内嵌样式 ###   
    用style 标签包裹着
### 外联样式 ###
    另起一个样式表文件 最后通过link 文件连入其中的。

## less ##
less 文件的引入之后，浏览器要以服务器的形式打开，不然效果出不来

要注意表明文件类型，否则不起作用。

```
<script id="template" type="text/html">

id 必须用双引号，不然会报错
```


## 表单 ##

表单聚焦时候线条去除	outline

## z-index ##

这个属性只对定位的元素有效

## box-shadow ##

##  background 
是一个符合属性，它的书写其实是有顺序要求的。如果你在前后者在后又给它设置单个属性，存在着覆盖问题。
## 白色与透明

## 浮动。
列出清除浮动的方法，并说明他们的优缺点。

## line-height
行高是有继承性的，如果一个父盒子里面有若干个子元素，那么他们都会去继承来自父盒子的行高。这样带来。
**这一点在是元素垂直居中的时候要 尤其注意**

## css 样式与模块化思想。
base.css 基础样式或者叫做重置样式
common.css 全局样式，**要让他的权重尽可能的低**，方便后续增加需求的时候对他进行覆盖
page.css ，页面独立样式，在vue 中，如果是添加了scode ，那么在这个页面上写的样式只会对这个页面有效。

##  less
定义变量
循环
函数

## less的编译原理


## 行内块元素并排时候，他们之间会有间隙，
解决办法，
1 浮动
2 定位
3 给父元素加上 font-size :0px;  **注意一定是父元素，不然没有效果**。


## > 子代选择器

如果我们只是想选择某个元素的一个后代作为要，那么就可以使用子代选择器。

## 后代选择器
少用，会大范围杀伤！！！
## 类名
给类名取名字不要太过于随意！！！

## 定位

定位只是根据元素当前所在的位置进行定位，所以，我们在给元素进行定位的时候一定要把margin 考虑进去。
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            position: absolute;
            top: 0px;
            left: 0px;
            width: 200px;
            height: 200px;
            background-color: pink;
            padding: 20px;
            margin: 100px;
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```






