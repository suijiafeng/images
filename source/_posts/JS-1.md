title: JS对象的动态特性
author: suijiafeng
tags: []
categories: []
date: 2017-01-14 01:09:00
---
## 对象的动态特性
可以动态地给对象添加属性和方法

### 添加方法
	 a 使用点语法
	 ```
	 var obj ={
	     name :'zs',
	     age:18
	 }
	 obj.name;// zs
	 ```
	 b 使用数组的特性 
	 ```
	obj['name'];/ zs
	
	
	obj[{}] ="sdsfs";
	obj["[object Object]"];
	//why

	obj[]  里面需要的是一个字符串
 
//所以会di把调用tostring()方法  obj[{}] ==>中的空对象 { }转换成 object Object 存放起来。

## 序列化
	var obj = {x:1,y:true,z:[1,2,3],c：null};
	JSON.stringify(obj);
	
	var obj1 = {val:undefined,a:NaN,b:Infinity,c:new Date()};
	JSON.stringify(obj1);

#### 把字符串转成对象
	var obj3 = JSON.parse('{"x":1}');
	box3.x;//1

#### 自定义 序列化

	```
	var obj ={
	    x:1,
	    y:2,
	    o:{
	        o1:1,
	        o2:2,
	        toJSON:function(){
	            return this.o1+this.o2;
	        }
	    }
	};
	JSON.stringify(obj);
	// "{"x":1,"y":2,"o":3}"
	
	```

## 其他对象方法
	
	```
	var obj ={x:1,y:2};
	obj.toString();//"[object Object]"
	//自定义toString 方法
	obj.toString = function(){return this.x+this.y};
	"result"+obj;//result 3
	//自定义valueOf方法
	obj.valueOf = function(){
	    return this.x+this.y+100;
	}
	"result"+obj;//103
	```



