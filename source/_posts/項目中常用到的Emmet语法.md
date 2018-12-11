title: 項目中常用到的Emmet语法
author: suijiafeng
tags: []
categories: []
date: 2018-05-13 22:45:00
---
Emmet (前身为 Zen Coding) 是一个能大幅度提高前端开发效率的一个工具，基本上，大多数的文本编辑器都会允许你存储和重用一些代码块，我们称之为“片段”。虽然片段能很好地推动你得生产力，但大多数的实现都有这样一个缺点：你必须先定义你得代码片段，并且不能再运行时进行拓展。

Emmet把片段这个概念提高到了一个新的层次：你可以设置CSS形式的能够动态被解析的表达式，然后根据你所输入的缩写来得到相应的内容。Emmet是很成熟的并且非常适用于编写HTML/XML 和 CSS 代码的前端开发人员，但也可以用于编程语言。
下面介紹幾種常見的Emmet語法：

#### 后代：> ####
缩写：nav>ul>li
	
	<nav>
	    <ul>
	        <li></li>
	    </ul>
	</nav>
兄弟：+
缩写：div+p+bq
	
	<div></div>
	<p></p>
	<blockquote></blockquote>
上级：^
缩写：div+div>p>span+em^bq
	
	<div></div>
	<div>
	    <p><span></span><em></em></p>
	    <blockquote></blockquote>
	</div>

分组：()
缩写：div>(header>ul>li*2>a)+footer>p

	<div>
	    <header>
	        <ul>
	            <li><a href=""></a></li>
	            <li><a href=""></a></li>
	        </ul>
	    </header>
	    <footer>
	        <p></p>
	    </footer>
	</div>

乘法：*
缩写：ul>li*5
	
	<ul>
	    <li></li>
	    <li></li>
	    <li></li>
	    <li></li>
	    <li></li>
	</ul>
自增符号：$
缩写：h$[title=item$]{Header $}*3
	
	<h1 title="item1">Header 1</h1>
	<h2 title="item2">Header 2</h2>
	<h3 title="item3">Header 3</h3>
#### ID和类属性 ####

缩写：#header

	<div id="header"></div>
缩写：.title

	<div class="title"></div>
缩写：form#search.wide

	<form id="search" class="wide"></form>
缩写：p.class1.class2.class3

	<p class="class1 class2 class3"></p>
自定义属性
缩写：p[title=”Hello world”]

	<p title="Hello world"></p>

文本：{}
缩写：a{Click me}

	<a href="">Click me</a>
    
缩写：p>{Click }+a{here}+{ to continue}

	<p>Click <a href="">here</a> to continue</p>
隐式标签
缩写：.class

    <div class="class"></div>
缩写：em>.class

    <em><span class="class"></span></em>
缩写：ul>.class

    <ul>
         <li class="class"></li>
    </ul>
缩写：table>.row>.col

	  <table>
	      <tr class="row">
	          <td class="col"></td>
	      </tr>
	  </table>
#### HTML ####
缩写：link:css

	  <link rel="stylesheet" href="" />


缩写：link:favicon

	<link rel="shortcut icon" type="image/x-icon" href="favicon.ico" />

缩写：link:touch

	<link rel="apple-touch-icon" href="favicon.png">


缩写：script:src

	<script src=""></script>

别名：input:radio

	<input type="radio" name="" id="" />


缩写：input:submit

	<input type="submit" value="" />
缩写：input:s

	<input type="submit" value="" />
缩写：input:image

	<input type="image" src="" alt="" />



商业转载请联系作者获得授权,非商业转载请注明出处。
原文: https://www.w3cplus.com/tools/emmet-cheat-sheet.html © w3cplus.com著作权归作者所有。