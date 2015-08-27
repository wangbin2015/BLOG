---
layout: post
title: 遇见的JavaScript高级技巧汇总
description: "遇见的JavaScript高级技巧汇总"
modified: 2015-08-27
category: JavaScript
tags: [JavaScript]
---

　　因个人知识有限，若发现文章中错误，欢迎发邮件与我进行讨论，邮箱：wangbin2014@hotmail.com，同时，欢迎关注[我的github账号](https://github.com/wangbin2015)                  　　        

***

####一、安全的类型检测

```javascript
		function type(obj){
        	return Object.prototype.toString.call(obj).slice(8,-1);
        }
```
类型检测方法：typeof、instanceof、Object.prototype.toString、constructor、duck type        
1. **typeof**运算符：返回一个字符串，适合基本类型和function的检测，遇到null失效(返回的是object)     
2. **instanceof**运算符：判断对象类型，是基于原型链完成判断的操作符，适合自定义对象，也可以用来检测原生对象，在不同iframe和window间检测时失效
3. **Object.prototype.toString**方法：适合内置对象和基元类型，遇到null/undefined失效，IE6/7/8返回"[object Object]"
4. **constructor**:重写了默认的prototype对象，constructor属性也就变成了新对象的constructor属性（指向Object构造函数），此时尽管instanceof操作符可以返回正确的结果，但是constructor已经无法确定对象的类型，用法事例：constructoralert((30).constructor)
5. **duck type**鸭子类型:不知道一个对象是不是数组，可以判断他的length是不是数字，是否有join push等方法，通过特征判断对象是否属于某个类型，这个方法也是比较常用到的

***

####二、作用域安全的构造函数
确保不使用new操作符时，this不被解析成window对象
```javascript
		function Person(name,age,job){
			if(this instanceof Person){
				this.name=name;
				this.age=age;
				this.job=job;
			}else{
				return new Person(name,age,job);
			}
		}
```
***

####三、函数绑定
```javascript
		var handler={
			message:'Event handled',
			handleClick:function(event){
				alert(this.message);
			}
		}
		var btn=document.getElementById('btn');
		EventUntil.addHandler(btn,'click',handler.handleClick.bind(handler));
```

