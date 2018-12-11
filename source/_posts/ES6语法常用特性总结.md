title: ES6语法常用特性总结
author: suijiafeng
tags: []
categories: []
date: 2018-08-20 23:18:06
---
ECMAScript6在保证向下兼容的前提下，提供大量新特性，目前浏览器兼容情况如下：

ES6特性如下：

### 块级作用域  ###

关键字let, 
常量const

blogexcerpt:123456789

### 对象字面量的属性赋值简写 ###

	var obj = {
	    // __proto__
	    __proto__: theProtoObj,
	    // Shorthand for ‘handler: handler’
	    handler,
	    // Method definitions
	    toString() {
	    // Super calls
	    return "d " + super.toString();
	    },
	    // Computed (dynamic) property names
	    [ 'prop_' + (() => 42)() ]: 42
	};

### 赋值解构 ###

	let singer = { first: "Bob", last: "Dylan" };
	let { first: f, last: l } = singer; // 相当于 f = "Bob", l = "Dylan"
	let [all, year, month, day] =  /^(\d\d\d\d)-(\d\d)-(\d\d)$/.exec("2015-10-25");
	let [x, y] = [1, 2, 3]; // x = 1, y = 2
    


4.函数参数（Default 、Rest 、Spread）

	//Default
	function findArtist(name='lu', age='26') {
	    ...
	}
	
	//Rest
	function f(x, ...y) {
	  // y is an Array
	  return x * y.length;
	}

	f(3, "hello", true) == 6
	
	//Spread
	function f(x, y, z) {
	  return x + y + z;
	}
	// Pass each elem of array as argument
	f(...[1,2,3]) == 6

### 箭头函数  ###


1. 简化了代码形式，默认return表达式结果。


1. 自动绑定语义this，即定义函数时的this。如上面例子中，forEach的匿名函数参数中用到的this。

#### 字符串模板 ####

	var name = "Bob", time = "today";
	`Hello ${name}, how are you ${time}?`
	// return "Hello Bob, how are you today?"

#### Iterators（迭代器）+ for..of	 ####

迭代器有个next方法，调用会返回：


1. 返回迭代对象的一个元素：{ done: false, value: elem }

1. 如果已到迭代对象的末端：{ done: true, value: retVal }

`	 for (var n of ['a','b','c']) {
	  console.log(n);
	}
	// 打印a、b、c
`

#### Class ####

Class，有constructor、extends、super，但本质上是语法糖（对语言的功能并没有影响，但是更方便程序员使用）。

	class Artist {
	    constructor(name) {
	        this.name = name;
	    }
	
	    perform() {
	        return this.name + " performs ";
	    }
	}


	class Singer extends Artist {
	
	    constructor(name, song) {
	        super.constructor(name);
	        this.song = song;
	    }
	
	    perform() {
	        return super.perform() + "[" + this.song + "]";
	    }
	}

	let james = new Singer("Etta James", "At last");
	james instanceof Artist; // true
	james instanceof Singer; // true
	
	james.perform(); // "Etta James performs [At last]"

#### Map + Set + WeakMap + WeakSet ####

四种集合类型，WeakMap、WeakSet作为属性键的对象如果没有别的变量在引用它们，则会被回收释放掉。
		
		// Sets
		var s = new Set();
		s.add("hello").add("goodbye").add("hello");
		s.size === 2;
		s.has("hello") === true;
		
		// Maps
		var m = new Map();
		m.set("hello", 42);
		m.set(s, 34);
		m.get(s) == 34;
		
		//WeakMap
		var wm = new WeakMap();
		wm.set(s, { extra: 42 });
		wm.size === undefined
		
		// Weak Sets
		var ws = new WeakSet();
		ws.add({ data: 42 });//Because the added object has no other references, it will not be held in the set
		12.Math + Number + String + Array + Object APIs

一些新的API
	
	Number.EPSILON
	Number.isInteger(Infinity) // false
	Number.isNaN("NaN") // false
	
	Math.acosh(3) // 1.762747174039086
	Math.hypot(3, 4) // 5
	Math.imul(Math.pow(2, 32) - 1, Math.pow(2, 32) - 2) // 2
	
	"abcde".includes("cd") // true
	"abc".repeat(3) // "abcabcabc"
	
	Array.from(document.querySelectorAll('*')) // Returns a real Array
	Array.of(1, 2, 3) // Similar to new Array(...), but without special one-arg behavior
	
	[0, 0, 0].fill(7, 1) // [0,7,7]
	[1, 2, 3].find(x => x == 3) // 3
	[1, 2, 3].findIndex(x => x == 2) // 1
	[1, 2, 3, 4, 5].copyWithin(3, 0) // [1, 2, 3, 1, 2]
	["a", "b", "c"].entries() // iterator [0, "a"], [1,"b"], [2,"c"]
	["a", "b", "c"].keys() // iterator 0, 1, 2
	["a", "b", "c"].values() // iterator "a", "b", "c"
	
	Object.assign(Point, { origin: new Point(0,0) })

####  Proxies ####

使用代理（Proxy）监听对象的操作，然后可以做一些相应事情。

		var target = {};
		var handler = {
		  get: function (receiver, name) {
		    return `Hello, ${name}!`;
		  }
		};
		
		var p = new Proxy(target, handler);
		p.world === 'Hello, world!';

可监听的操作：

 get、set、has、deleteProperty、apply、construct、getOwnPropertyDescriptor、defineProperty、getPrototypeOf、setPrototypeOf、enumerate、ownKeys、preventExtensions、isExtensible。

#### Symbols ####

Symbol是一种基本类型。Symbol 通过调用symbol函数产生，它接收一个可选的名字参数，该函数返回的symbol是唯一的。

		var key = Symbol("key");
		var key2 = Symbol("key");
		key == key2  //false

#### Promises ####

Promises是处理异步操作的对象，使用了 Promise 对象之后可以用一种链式调用的方式来组织代码，让代码更加直观（类似jQuery的deferred 对象）。
		
		function fakeAjax(url) {
		  return new Promise(function (resolve, reject) {
		    // setTimeouts are for effect, typically we would handle XHR
		    if (!url) {
		      return setTimeout(reject, 1000);
		    }
		    return setTimeout(resolve, 1000);
		  });
		}
		
		// no url, promise rejected
		fakeAjax().then(function () {
		  console.log('success');
		},function () {
		  console.log('fail');
		});

总结
对于ES6，在某些方式是不是重蹈ES4的覆辙，变得复杂了；又或许几年后大家的接受能力变强了，觉得是应该这样了。我觉得还是不错的，因为它们是向下兼容的，即使复杂语法不会用，也能用自己熟知的方式，提供的语法糖也都挺实际。