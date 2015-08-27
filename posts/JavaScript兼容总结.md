---
layout: post
title: JavaScript兼容总结
description: "JavaScript兼容总结"
modified: 2015-08-27
category: JavaScript
tags: [JavaScript]
---

　　因个人知识有限，若发现文章中错误，欢迎发邮件与我进行讨论，邮箱：wangbin2014@hotmail.com，同时，欢迎关注[我的github账号](https://github.com/wangbin2015)     

***
######1、document.formName.item("itemName") 问题
*说明：*IE下,可以使用`document.formName.item("itemName")`或`document.formName.elements["elementName"]`
Firefox下，只能使用`document.formName.elements["elementName"]`        
*解决方法：*统一使用`document.formName.elements["elementName"]`

######2、集合类对象问题
*说明：*IE下,可以使用()或[]获取集合类对象;Firefox下,只能使用[]获取集合类对象       
*解决方法：*统一使用[]获取集合类对象   

######3、自定义属性问题
*说明：*IE下,可以使用获取常规属性的方法来获取自定义属性,也可以使用getAttribute()获取自定义属性，Firefox下，只能使用getAttribute()获取自定义属性     
*解决方法：*统一通过getAttribute()获取自定义属性，不过更推荐直接通过“点”运算符访问元素属性

######4、eval("idName")问题
*说明：*IE下,可以使用`eval("idName")`或`getElementById("idName")`来取得id为idName的HTML对象，Firefox下只能使用`getElementById("idName")`来取得id为idName的HTML对象     
*解决方法：*统一用`getElementById("idName")`来取得id为idName的HTML对象

######5、变量名与某HTML对象ID相同的问题
*说明：*IE下,HTML对象的ID可以作为document的下属对象变量名直接使用;Firefox下则不能.Firefox下,可以使用与HTML对象ID相同的变量名;IE下则不能      
*解决方法：*使用`document.getElementById("idName")`代替`document.idName`，最好不要取HTML对象ID相同的变量名，以减少错误;在声明变量时，一律加上var,以避免歧义

######6、const问题
*说明：*Firefox下,可以使用const关键字或var关键字来定义常量，IE下，只能使用var关键字来定义常量
*解决方法：*统一使用var关键字来定义常量

######7、input.type属性问题
*说明：*IE下input.type属性为只读，但是Firefox下`input.type`属性为读写     
*解决方法：*可以创建两个输入框，比如平时咱们有密码框，想通过把type为password的值改为text，IE下是不允许的

######8、window.event问题
*说明：*`window.event`只能在IE下运行，而不能在Firefox下运行,这是因为Firefox的event只能在事件发生的现场使用。Firefox必须从源处加入event作参数传递。IE忽略该参数，用window.event来读取该event      
*解决方法：* `var e = e || window.event；`

######9、event.x与event.y问题
*说明：*IE下，even对象有x,y属性,但是没有pageX，pageY属性；Firefox下，even对象有pageX，pageY属性，但是没有x,y属性    
*解决方法：*使用`var x = e.x ? e.x : e.pageX; `来代替IE下的`event.x`或者Firefox下的`e.pageX`；

######10、event.srcElement问题
*说明：* IE下,event对象有srcElement属性,但是没有target属性;Firefox下,even对象有target属性,但是没有srcElement属性。
*解决方法：*使用`obj(obj = event.srcElement ? event.srcElement : event.target;)`来代替IE下的`event.srcElement`或者Firefox下的`event.target`，请同时注意event的兼容性问题

######11、body问题
*说明：*Firefox的body在body标签没有被浏览器完全读入之前就存在；而IE的body则必须在body标签被浏览器完全读入之后才存在

######12、firefox与IE的父元素(parentElement)的区别
*说明：*IE支持`parentElement`和`parentNode`获取父节点，而FF只能使用后者      
*解决方法：*统一使用`parentNode`；

######13、innerText问题
*说明：*`innerText`在IE中能正常工作，但是`innerText`在FireFox中却不行. 需用`textContent`       
*解决方法：*`elem.innerText = elem.textContent = “值”`  

######14、样式单位问题
*说明：*FireFox中设置HTML标签的`style`时，所有位置性和字体尺寸的值必须后跟px。这个ie也是支持的

######15、样式关键字冲突问题
*说明：*CSS属性与Javascript中的保留关键字命名相同，IE中style+属性，非IE中css+属性

######16、class属性冲突问题
*说明：*`class`属性冲突，`class`是javascript中的保留关键字

######17、年份获取问题
*说明：*使用`getFullYear`替换`getYear`

######18、for属性冲突问题
*说明：*`lable`标签的属性`for`冲突，在IE浏览器中`getAttribute(“htmlFor”)`，在非IE浏览器中`getAttribute(“for”)`

######19、removeChild和removeNode的问题
*说明：*`appendNode`在IE和Firefox下都能正常使用，但是`removeNode`只能在IE下用，FF支持`removeChild`

######20、事件监听函数的问题
*说明：*标准浏览器的写法`addEventListener()`和IE的写法`attachEvent() `    
*解决方法：*判断`addEventListener`是否存在，如果存在则用否则用IE8以下的版本（含IE8）的绑定方法`attachEvent，removeEventListener()`和`detachEvent()`也是一样的用法

######21、阻止事件冒泡
*说明：* `stopPropagation()`和`cancelBubble`，前者是方法，是标准的写法，后者是属性，赋值`true`表示阻止，是IE的写法      
*解决方法：*判断`stopPropagation`是否存在，如果存在则用标准写法否则则用IE的写法，不可反过来判断

######22、阻止默认事件
*说明：* `preventDefault()`和`returnValue()`前者标准写法，后者IE写法      
*解决方法：*一般情况建议直接使用`return false`阻止，但和取消默认事件的含义是不同的
