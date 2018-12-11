title: css选择器的使用
author: suijiafeng
tags: []
categories: []
date: 2016-09-19 01:13:00
---
#CSS选择器#
## 交集选择器 （需要满足他的条件。） ##


## 后代选择器 ##
main p
只要是 main 的后代 p元素，都会选中

## 子代选择器 ##


## 并集选择器，即群组选择器 ##
以逗号隔开


## 相邻选择器即同辈选择器也叫毗邻选择器  M+N 
选择M元素后面的一个兄弟N元素

```
特殊情况：
<style type="text/css">
    li + li {
        color:red;
    }
</style>

<div>
  <ul>
    <li>List item 1</li>
    <li>List item 2</li>
    <li>List item 3</li>
  </ul>
</div>

效果：
  <li>List item 2</li>
  <li>List item 3</li>
    文字变红
```

## 同辈组合选择器即兄弟选择器   M~N 
选择M元素后面的所有兄弟N元素


# 选择器的权重 
- 在复合选择的时候，权重越高，优先级权重越高。

### 优选级顺序:
 - 继承性<通配 符<标签选择器<类选择器<ID选择器<行内样式<!important
注意：！important影响的只是他的单一属性而已。


## 伪类选择器 ##
li:first-child:控制第一个子元素   (重要)
li:last-child：控制最后一个子元素（重要)
其它：（了解即可）
li:nth-child(2:)控制特定的某一个元素(控制第二个)
li:nth-child(odd):控制奇数的子元素
li:nth-child(even):控制偶数的子元素
li:nth-child(n+2):
li:nth-child(2n+1)
li:nth-child()

## link伪类学习
- a:hover  当鼠标悬停在a标签上的时候
- a:active  当鼠标点下去但没有松开的时候（激活状态）
- a:link    a标签未被访问过的样式（不常用）

- a:visited    a标签访问后的样式。
	 注意：当四个伪类同事作用在一个a标签上的时候：
爱恨原则：love hate:link visited hover active;（顺序是否错了）
并不是a标签才能使用伪类，其它的标签一样可以使用。
	子盒子所在的区域同时也是父盒子的那个区域。

- a:focus ，当表单空间获得焦点的时候