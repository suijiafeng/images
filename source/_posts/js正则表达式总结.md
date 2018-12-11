title: js 正则表达式总结
author: suijiafeng
tags: []
categories: []
date: 2018-06-5 22:45:00
---

## 1. 简介 


正则表达式(Regular Expression) 是对字符串操作的一种逻辑公式，就是用事先定义好的一些特定字符、及这些特定字符的组合，组成一个规则字符串，这个规则字符串用来表达对字符串的一种过滤逻辑。

简单来说就是：按照某种规则去匹配符合条件的字符串。正则表达式的规则是/ pattern / flags

可以使用字面量形式或者new的方式来创建正则表达式

	// 使用直接字面量创建，推荐使用，性能更好，注意这里pattern不能为空，不然以为是注释
	var exp1 = /\d/g
	// 使用RegExp对象创建
	var exp2 = new RegExp('\d', 'g');
模式中使用的所有元字符都建议在之前加\转义，正则表达式中的元字符包括：
	
	( [ { \ ^ $ | ) ? * + . ] }

## 2. 内容 

### 2.1 匹配模式 
修饰符表示正则表达式的匹配模式
	
	修饰符	描述
	i	执行对大小写不敏感的匹配
	g	执行全局匹配，查找所有匹配而非在找到第一个匹配后停止
	m	执行多行匹配，会改变^和$的行为
	u	可以匹配4字节的unicode编码
	加了u修饰符，会正确处理大于\uFFFF的unicode，比如4字节的?\uD83D\uDC2A
	
	/^\uD83D/.test('\uD83D\uDC2A')                // true
	/^\uD83D/u.test('\uD83D\uDC2A')                // false

### 2.2 类 
类使用[ ]来表达，用于查找某个范围内的字符
	
	表达式	描述
	[abc]	查找方括号之间的任何字符
	[0-9]	查找任何从 0 至 9 的数字
	还有一些预定义类方便我们直接使用：
	
	预定义类	等价	描述
	\s	[\t\n\x0B\f\r]	空格
	\S	[^\t\n\x0B\f\r]	非空格
	\d	[0-9]	数字
	\D	[^0-9]	非数字
	\w	[a-zA-Z_0-9]	单词字符 ( 字母、数字、下划线)
	\W	[^a-zA-Z_0-9]	非单词字符
	.	[^\r\n]	任意字符，除了回车与换行外所有字符
	\f	\x0c \cL	匹配一个换页符
	\n	\x0a \cJ	匹配一个换行符
	\r	\x0d \cM	匹配一个回车符
	\t	\x09 \cI	匹配一个制表符
	\v	\x0b \cK	匹配一个垂直制表符
	\xxx	
	查找以八进制数 xxx 规定的字符
	\xdd	
	查找以十六进制数 dd 规定的字符
	\uxxxx	
	查找以十六进制数 xxxx 规定的 Unicode 字符

### 2.3 量词 
量词表示匹配多少个目标对象，精确匹配长度使用{ }
	
	量词	等价	描述
	n*	{0,}	匹配零个或多个n
	n+	{1,}	匹配至少一个 n 的字符串
	n?	{0,1}	匹配零个或一个n
	{n}	
	匹配n次
	{n,m}	
	匹配n到m次
	{n,}	
	至少匹配n次
	
### 2.4 边界 

	边界	描述
	^	以xx开始，在类[ ]中表示非
	$	以xx结束
	\b	单词边界
	\B	非单词边界
	 ^ 匹配字符串开始位置，也就是位置0，如果设置了 RegExp 对象的 Multiline 属性 m ，^ 也匹配 'n' 或 'r' 之后的位置
	 $ 一般匹配字符串结束位置，如果设置了 RegExp 对象的 Multiline 属性m ，$  也匹配 'n' 或 'r' 之前的位置
	 \b 匹配一个单词边界，也就是指单词和空格间的位置，如er\b可以匹配"never" 中的 'er'，但不能匹配 "verb" 中的 'er'
	 \B 匹配非单词边界。如er\B能匹配 "verb" 中的 'er'，但不能匹配 "never" 中的 'er'

### 2.5 分组 
分组使用( )，作用是提取相匹配的字符串，使量词作用于分组
比如hehe{3}是把e匹配了3次而不是单词，如果希望作用于单词，可以使用分组(hehe){3}

或
分组中使用 | 可以达到或的效果
比如：T(oo|ii)m可以匹配 Toom 和 Tiim
	
	`abToomhaTiimmm`.replace(/T(oo|ii)m/g, '-') // ab-ha-mm

反向引用
使用( )后可以使用$1-$9等来匹配
	
	'2018-02-11'.replace(/(\d{4})\-(\d{2})\-(\d{2})/g, '$2/$3/$1') // 02/11/2018

后向引用
\n 表示后向引用，\1是指在正则表达式中，从左往右数第1个( )中的内容；以此类推，\2表示第2个( )，0表示整个表达式。
	
	//匹配日期格式，表达式中的\1代表重复(\-|\/|.)
	var rgx = /\d{4}(\-|\/|.)\d{1,2}\1\d{1,2}/
	rgx.test("2016-03-26")             // true
	rgx.test("2016-03.26")             // false
后向引用和反向引用的区别是：\n只能用在表达式中，而$n只能用在表达式之外的地方。

忽略分组
如果不希望捕获某些分组，在分组内加上?:即可
比如(?:tom).(ok)那么这里$1指的就是ok

前瞻
前瞻是RegExp匹配到规则的时候，向后检查是否符合断言，后顾JS目前不支持

	名称	正则	描述
	正向前瞻	(?= )	后面要有xx
	负向前瞻	(?! )	后面不能有xx
	'1a2bc*456v8'.replace(/\w(?=\d)/g, '-')        
	// 1-2bc*--6-8   匹配后面是数字的单词字符
	'1a2bc*456v8'.replace(/\w(?!\d)/g, '-')            
	// -a---*45-v-   匹配后面不是数字的单词字符
	(?=exp)匹配一个位置，这个位置的右边能匹配表达式exp，注意这个表达式仅仅匹配一个位置，只是它对于这个位置的右边有要求，而右边的东西是不会被放进结果的，比如用read(?=ing)去匹配"reading"，结果是"read"，而"ing"是不会放进结果的。
	
	举个栗子，对密码应用以下限制：其长度必须介于 4 到 8 个字符之间，并且必须至少包含一个数字，正则是/^(?=.*\d).{4,8}$/

### 2.6 贪婪模式 与 非贪婪模式 
正则表达式在匹配的时候默认会尽可能多的匹配，叫贪婪模式。通过在限定符后加? 可以进行非贪婪匹配

	比如\d{3,6}默认会匹配6个数字而不是3个，在量词{ }后加一个? 就可以修改成非贪婪模式，匹配3次	
	`12345678`.replace(/\d{3,6}/, '-')                // -78
	`12345678`.replace(/\d{3,6}?/, '-')                // -45678
	'abbbb'.replace(/ab+?/, '-')                // -bbb

### 2.7 优先级 
优先级从高到低：
	
	转义 \
	括号( )、(?: )、(?= )、[ ]
	字符和位置
	或 |
	


## 3. 常用属性与方法 

3.1 RegExp构造函数属性
RegExp构造函数上也包含一些属性，这些属性适用于作用域中所有的正则表达式，并且基于所执行的最近一次正则表达式操作而变化，这些属性分别有一个长属性名和短属性名
	
	长属性名	短属性名	描述
	input	$_	返回执行规范表述查找的字符串。只读
	lastMatch	$&	返回任何正则表达式搜索过程中的最后匹配的字符。只读
	lastParen	$+	如果有的话，返回任何正则表达式查找过程中最后括的子(分组)匹配。只读
	leftContext	$`	返回被查找的字符串中从字符串开始位置到最后匹配之前的位置之间的字符。只读
	rightContext	$'	返回被搜索的字符串中从最后一个匹配位置开始到字符串结尾之间的字符。只读

### 3.2 RegExp实例上的属性 
属性	描述
	global	是否全文搜索，默认false，对应修饰符的g，只读
	ignoreCase	是否大小写敏感，默认false，对应修饰符i，只读
	multiline	是否多行搜索，默认false，对应修饰符m，只读
	flags	返回修饰符，只读
	lastIndex	当前表达式匹配内容的最后一个字符的下一个位置
	source	正则表达式的文本字符串

### 3.3 常用方法 
方法详细的探究可以看一下文章JS 进阶- test, exec, match, replace

RegExp.prototype.test(str)
测试字符串参数中是否存在匹配正则表达式的字符串，使用.test的时候如果修饰符有g，那么会正则会记住lastIndex并在下一次执行的时候从lastIndex处开始检测，如果只是为了测试是否符合正则，可以不用g或者每次都重新实例化正则表达式
	
	const reg=/\w/g
	reg.test('a')                        // true
	reg.test('a')                        // false
	RegExp.prototype.exec(str)
使用正则表达式对字符串执行搜索，并将更新全局RegExp对象的属性以反映匹配结果
如果匹配失败，exec() 方法返回 null
如果匹配成功，exec() 方法返回一个数组，并更新正则表达式对象的属性

数组索引0：匹配的全部字符串
数组索引1,2..n：括号中的分组捕获
index：属性是匹配文本的第一个字符的位置
input：存放被检索的字符串
要注意的是：

exec()永远只返回一个匹配项（指匹配整个正则的）

如果设置了g修饰符，每次调用exec()会在字符串中继续查找新匹配项，不设置g修饰符，对一个字符串每次调用exec()永远只返回第一个匹配项。所以如果要匹配一个字符串中的所有需要匹配的地方，那么可以设置g修饰符，然后通过循环不断调用exec方法。


	//匹配所有ing结尾的单词
	const str="Reading and Writing"
	const pattern=/\b([a-zA-Z]+)ing\b/g
	let matches
	while(matches=pattern.exec(str)){
	  console.log(matches.index +' '+ matches[0] + ' ' + matches[1]);
	}
	// 0 Reading Read
	// 12 Writing Writ
	
	String.prototype.search(reg)

search() 方法用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串
方法返回第一个匹配结果的index，查找不到返回-1
search() 方法不执行全局匹配，它将忽略修饰符g，并且总是从字符串的开始进行检索

String.prototype.split(reg)
split() 方法一般用来分割字符串成数组，也可以传入正则表达式，使用正则可以避免一些传入字符串解决不了的问题
	
	'a1b2c3d4e'.split(/\d/)            // ["a", "b", "c", "d", "e"]
	'a b   c'.split(' ')               // ['a', 'b', '', '', 'c']   无法识别连续空格
	'a b   c'.split(/\s*/)             // ['a', 'b', 'c']
	String.prototype.match(reg)
match() 方法将检索字符串，以找到一个或多个与reg相匹配的文本，reg是否有修饰符g影响很大
返回值与RegExp.prototype.exec的返回类似，不过只返回匹配的字符串数组
	
	'cdbbdbsdbdbzddzdbbbd'.match(/d(b+)d/g)     //  ["dbbd", "dbd", "dbbbd"]
	'cdbbdbsdbdbzddzdbbbd'.match(/d(b+)d/)     //  ["dbbd", "bb", index: 1, input: "cdbbdbsdbdbzddzdbbbd"]
如果修饰符有g 则匹配出所有匹配的数组，如果不是，则出第一个匹配的字符串，以及相应的捕获内容

	String.prototype.replace(reg, str | num | function)
找到匹配并替换，传入string、number比较常见，这里传入回调function是比较高级的用法，这里可以参考MDN

比如一个场景，把手机号的中间4位换成*
	
	function validateMobile(str) {
	  return /^[1][0-9]{10}$/.test(str) && str.replace(/(\d{3})(\d{4})(\d{4})/, (rs, $1, $2, $3) => `${$1}****${$3}`)
	}
也可以不返回值，用回调来遍历，比如一个在面试中会遇到的问题：找出重复最多的字符
	
	let str = 'asss23sjdssskssa7lsssdkjsssdss'
	const arr = str.split(/\s*/)   // 把字符串转换为数组
	const str2 = arr.sort().join('')      // 首先进行排序，这样结果会把相同的字符放在一起，然后再转换为字符串
	let value = ''
	let index = 0
	str2.replace(/(\w)\1*/g, function($0, $1) {         //匹配字符
	  if (index < $0.length) {
	    index = $0.length              // index是出现次数
	    value = $1                 // value是对应字符
	  }
	})
	console.log(`最多的字符: ${value} ,重复的次数: ${index}`)         // s 17



商业转载请联系作者获得授权,非商业转载请注明出处。
原文: https://mp.weixin.qq.com/s/_ub6XtBuL4ouJFfZ96cfwg  著作权归 © 微信公众号 “前端大杂烩” 作者所有。